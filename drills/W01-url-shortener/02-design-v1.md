# W01 URL Shortener - Design v1 (샘플)

> 형식 예시용 최소 샘플입니다. 초안은 사람이 직접 채운다는 가정으로 작성합니다.

## 1) 아키텍처 개요
- 한 줄 요약: API 서비스 + 키 생성기 + KV 저장소 + 캐시 조합
- 시스템 경계: 링크 생성/조회/리다이렉트 처리
- 핵심 가정: 조회 트래픽이 쓰기보다 훨씬 크다

## 2) 컴포넌트 책임
| 컴포넌트 | 책임 | 입력 | 출력 | 상태 보유 |
|---|---|---|---|---|
| API Service | 생성/조회 API 처리 | HTTP 요청 | 단축 URL/원본 URL | 없음 |
| Key Generator | 고유 short key 발급 | 생성 요청 | short key | 시퀀스 상태 |
| KV Store | key -> URL 매핑 저장 | key, URL | 조회 결과 | 있음 |
| Cache | 인기 key 캐싱 | key | URL | 있음 |

## 3) 데이터 흐름
1. 생성 요청 수신
2. 키 생성 후 KV Store 저장
3. 조회 시 캐시 확인 후 미스면 KV 조회
4. 원본 URL로 302 리다이렉트

## 4) API / 이벤트 계약
| 유형 | 이름 | 요청/페이로드 | 응답/결과 | Idempotency |
|---|---|---|---|---|
| API | POST /v1/shorten | {"url": "..."} | {"shortUrl": "..."} | 선택(요청키 기반) |
| API | GET /{key} | path key | 302 redirect | 해당 없음 |

## 5) 데이터 모델
| 엔터티 | 키 | 주요 필드 | 인덱스 | TTL/보존 |
|---|---|---|---|---|
| UrlMap | short_key | original_url, created_at, expire_at | short_key PK | expire_at 선택 |

## 6) 스케일 / 장애 가정
- 읽기 확장 전략: 캐시 수평 확장
- 쓰기 확장 전략: key range 분산
- 단일 장애점 후보: Key Generator
- 장애 시 우선 보호 기능: 리다이렉트 읽기 경로

## 7) 리스크 및 미결정
- Risk 1: 핫키로 인한 캐시 편중
- Risk 2: 악성 URL 유입
- 미결정 항목: 사용자 지정 키 정책
