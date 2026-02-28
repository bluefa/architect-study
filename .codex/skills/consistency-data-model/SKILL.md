---
name: consistency-data-model
description: Validate consistency model and data model alignment in drills/*/02-design-v1.md and drills/*/04-design-v2.md against requirements. Use when design files change and consistency/data findings must be written to reviews/topic-review.md.
---

# Consistency & Data Model

## Inputs
- Changed file: `drills/*/02-design-v1.md` or `drills/*/04-design-v2.md`
- Context files:
- `${DRILL_DIR}/01-requirements.md`
- `${DRILL_DIR}/02-design-v1.md`
- `${DRILL_DIR}/04-design-v2.md` (if exists)

## Procedure
1. Resolve `DRILL_DIR`, `TOPIC`, `REVIEW_FILE`.
2. Compare declared consistency level with API/event behavior.
3. Check keys, indexes, idempotency policy, ordering/duplication handling.
4. Identify mismatch between data model and operational behavior.

## Output
- Update `REVIEW_FILE` section: `Consistency & Data`
- Add findings with: `observation`, `risk`, `required change`

## Fail Gate
Mark as fail if one of the following is true.
- Consistency policy conflicts with API contract.
- Idempotency policy is absent for write API.
- Key/index strategy does not support access pattern.
