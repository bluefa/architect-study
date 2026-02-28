# W01 URL Shortener - Design v2 (샘플)

> 형식 예시용 최소 샘플입니다. v1에서 리뷰 반영한 수정본 형태를 보여줍니다.

## 0) v1 대비 수정 요약
| 항목 | v1 | v2 변경 |
|---|---|---|
| 키 발급 | 단일 발급기 | 발급기 이중화 + 장애 시 랜덤 키 fallback |
| 캐시 | 일반 캐시 조회 | 핫키 보호를 위한 짧은 TTL + 백오프 |
| 관측성 | 기본 로그 | 생성/리다이렉트 SLI 및 경보 조건 추가 |

## 1) 아키텍처 개요
- 한 줄 요약: 읽기 안정성 우선 구조 + 발급기 장애 대비 경로 추가
- 시스템 경계: 생성/조회/리다이렉트 + 기본 모니터링
- 핵심 가정: 읽기 우선, 생성 장애는 제한적으로 허용

## 2) 컴포넌트 책임
| 컴포넌트 | 책임 | 입력 | 출력 | 상태 보유 |
|---|---|---|---|---|
| API Service | 생성/조회 처리, fallback 라우팅 | HTTP 요청 | 응답/리다이렉트 | 없음 |
| Key Generator Cluster | 기본 키 발급 | 생성 요청 | short key | 시퀀스 상태 |
| KV Store | key-url 저장 | key, URL | 조회 결과 | 있음 |
| Cache | 조회 가속/핫키 완충 | key | URL | 있음 |

## 3) 데이터 흐름
1. 생성 요청은 기본 발급기로 처리, 실패 시 fallback 발급 경로 사용
2. 저장 성공 후 단축 URL 반환
3. 조회는 캐시 우선, 미스 시 KV 조회 후 캐시 적재
4. 오류율 상승 시 읽기 경로 보호 모드 활성화

## 4) API / 이벤트 계약
| 유형 | 이름 | 요청/페이로드 | 응답/결과 | Idempotency |
|---|---|---|---|---|
| API | POST /v1/shorten | {"url":"...","requestId":"..."} | {"shortUrl":"..."} | requestId 기준 |
| API | GET /{key} | path key | 302 redirect | 해당 없음 |

## 5) 데이터 모델
| 엔터티 | 키 | 주요 필드 | 인덱스 | TTL/보존 |
|---|---|---|---|---|
| UrlMap | short_key | original_url, created_at, expire_at | short_key PK | expire_at |
| RequestDedup | request_id | short_key, created_at | request_id PK | 24h |

## 6) 스케일 / 장애 가정
- 읽기 확장 전략: 캐시 수평 확장, 핫키 보호
- 쓰기 확장 전략: 발급기 shard 또는 fallback 경로
- 단일 장애점 후보: 중앙 KV 계층
- 장애 시 우선 보호 기능: 리다이렉트 처리 성공률 유지

## 7) 리스크 및 미결정
- Risk 1: fallback 키 충돌률 관리 필요
- Risk 2: 악성 URL 필터 성능 영향
- 미결정 항목: 분석 로그 파이프라인 도입 시점
