---
name: tradeoff-enforcement
description: Enforce explicit tradeoff documentation in drills/*/03-tradeoffs.md with alternatives, decision rationale, costs, risks, and rollback/migration plan. Use when tradeoff docs are created or edited and gaps must be written to reviews/topic-review.md.
---

# Tradeoff Enforcement

## Inputs
- Changed file: `drills/*/03-tradeoffs.md`
- Context files:
- `${DRILL_DIR}/02-design-v1.md`
- `${DRILL_DIR}/03-tradeoffs.md`

## Procedure
1. Resolve `DRILL_DIR`, `TOPIC`, `REVIEW_FILE`.
2. Verify at least two alternatives are compared (A vs B).
3. Validate decision rationale links to constraints/metrics.
4. Check cost, ops burden, complexity, risk, rollback/migration coverage.

## Output
- Update `REVIEW_FILE` section: `Tradeoff Gaps`
- For each missing element, add concrete fix instructions.

## Fail Gate
Mark as fail if one of the following is true.
- No alternative comparison.
- Decision rationale is qualitative only with no constraint linkage.
- Rollback or migration plan is missing.
