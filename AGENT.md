# AGENT Guide

## 목적
이 레포의 AI는 설계 대행자가 아니라 리뷰어/편집자/검증자입니다. 주간 Drill 산출물이 빠짐없이 쌓이도록 돕습니다.

## AI 사용 규칙
- 금지 구간:
  - `01-requirements.md` 초안 작성 대행 금지
  - `02-design-v1.md` 초안 작성 대행 금지
- 허용 역할:
  - 요구사항 누락/모순 검증
  - 병목/장애 시나리오 점검
  - 트레이드오프 문서 강제
  - 질문 생성, 액션 아이템 정리, 문서 구조 개선
- 원칙:
  - AI 제안은 "선택지"로만 제공
  - 최종 결정은 사람이 기록 (ADR)

## 폴더 구조
- `templates/`: 주차 산출물 템플릿
- `drills/Wxx-topic/`: 주차별 문제 풀이
- `reviews/`: AI 리뷰 결과 기록
- `adrs/`: 공통 ADR 인덱스/요약
- `concepts/`: 개념 카드 누적
- `artifacts/`: 다이어그램, 벤치마크, 기타 산출물
- `.agents/skills/`: Codex 스킬 정의(권장 경로)
- `.codex/skills/`: 스킬 미러 경로(환경 호환)

## 주간 루틴
1. Requirements 작성 (사람)
2. Design v1 작성 (사람, AI 금지)
3. Tradeoffs 작성 (사람)
4. AI Review 수행 (에이전트, `.agents/skills/*/SKILL.md` 규칙 적용)
5. Design v2 작성 (사람, 리뷰 반영)
6. ADR 1~3개 작성 (사람)

- 권장 시간: 주당 6~8시간
- 커밋 규칙:
  - `Wxx topic v1`
  - `Wxx topic v2 + ADR`

## Definition of Done
다음을 모두 만족해야 완료입니다.
- 필수 파일 5종(Requirements, v1, Tradeoffs, v2, ADR) 존재
- Tradeoffs 문서에 선택 근거/리스크/롤백 계획 명시
- 리뷰 문서에 병목/장애 시나리오/질문/액션 아이템 포함
- v2에 리뷰 반영 내역 명시
- 개념 카드 1개 이상 추가

## 필수 검증 질문 세트
- 요구사항:
  - 목표/비목표가 분리되었는가?
  - SLO/SLA와 트래픽 가정이 수치로 명시되었는가?
- 아키텍처:
  - 병목 지점은 어디이며 완화 전략이 있는가?
  - 데이터 정합성 모델(강/약/최종)이 API 계약과 일치하는가?
- 운영:
  - 장애 시 부분 장애/전면 장애 대응이 정의되었는가?
  - 관측성(로그/메트릭/트레이싱)과 경보 기준이 있는가?
- 의사결정:
  - 대안 비교와 선택 이유가 비용/복잡도/리스크 관점에서 설명되었는가?
  - 롤백 또는 마이그레이션 경로가 명시되었는가?

## 파일 네이밍 규칙
- 주차 폴더: `drills/Wxx-topic-name/`
- 주차 산출물:
  - `01-requirements.md`
  - `02-design-v1.md`
  - `03-tradeoffs.md`
  - `04-design-v2.md`
  - `05-adr-00n.md`
- 리뷰 파일: `reviews/Wxx-topic-review.md`
- 개념 카드: `concepts/YYYY-MM-DD-topic-concept.md`
- ADR 제목: `ADR-00n-short-title`
