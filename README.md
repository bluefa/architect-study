# System Design Drill Lab

시스템 설계 실력을 높이기 위한 주간 Drill 중심 학습 레포입니다.

## 왜 Drill 중심인가
- 설계는 읽는 것보다 직접 선택하고 기록할 때 실력이 빨리 늡니다.
- 매주 동일한 산출물 구조를 반복하면 비교/회고가 쉬워집니다.
- 설계에는 정답이 없으므로, 트레이드오프를 문서로 남겨야 판단력이 쌓입니다.
- AI는 설계를 대신하지 않고, 리뷰어/편집자/검증자로 활용합니다.

## 사용법 (주간 루틴)
1. Step 1: Requirements 작성 (사람)
2. Step 2: Design v1 작성 (사람, AI 금지)
3. Step 3: Tradeoffs 작성 (사람)
4. Step 4: AI Review 수행 (에이전트)
5. Step 5: Design v2 작성 (사람, 리뷰 반영)
6. Step 6: ADR 1~3개로 주요 결정 고정 (사람)

- 권장 시간: 주당 6~8시간
- 커밋 규칙:
  - `Wxx topic v1`
  - `Wxx topic v2 + ADR`

## 완료 기준 (DoD)
아래 최소 산출물이 모두 있어야 해당 주차를 완료로 인정합니다.
- `drills/Wxx-topic/01-requirements.md`
- `drills/Wxx-topic/02-design-v1.md`
- `drills/Wxx-topic/03-tradeoffs.md`
- `drills/Wxx-topic/04-design-v2.md`
- `drills/Wxx-topic/05-adr-001.md` (필요 시 추가 ADR)
- `reviews/Wxx-topic-review.md` (AI 리뷰 결과)
- `concepts/YYYY-MM-DD-topic-concept.md` (핵심 개념 카드 1장 이상)

## 시작 순서
1. `templates/` 파일을 복사해 새 주차 폴더를 만듭니다.
2. 사람 작성 구간(요구사항, v1, 트레이드오프)을 먼저 채웁니다.
3. AI 리뷰 스킬(`.agents/skills/*/SKILL.md`, 호환: `.codex/skills/*/SKILL.md`)과 `skills.md` 인덱스를 기준으로 리뷰를 수행하고, v2/ADR로 마무리합니다.
