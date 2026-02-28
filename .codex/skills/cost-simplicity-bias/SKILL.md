---
name: cost-simplicity-bias
description: Apply cost and simplicity bias to drills/*/04-design-v2.md by identifying over-engineering and proposing simpler alternatives with explicit impact. Use when v2 changes and cost/simplicity findings must be written to reviews/topic-review.md.
---

# Cost & Simplicity Bias

## Inputs
- Changed file: `drills/*/04-design-v2.md`
- Context files:
- `${DRILL_DIR}/02-design-v1.md`
- `${DRILL_DIR}/03-tradeoffs.md`
- `${DRILL_DIR}/04-design-v2.md`

## Procedure
1. Resolve `DRILL_DIR`, `TOPIC`, `REVIEW_FILE`.
2. Flag components with high complexity and low near-term value.
3. Propose a simpler alternative and describe what is deferred.
4. Estimate operational/cost impact qualitatively or numerically.

## Output
- Update `REVIEW_FILE` section: `Cost/Simplicity`
- Record each recommendation with keep/remove/defer decision.

## Fail Gate
Mark as fail if one of the following is true.
- Recommendation increases complexity without clear benefit.
- Cost or ops impact is not stated.
- No defer/remove candidate is identified.
