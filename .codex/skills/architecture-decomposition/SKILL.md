---
name: architecture-decomposition
description: Review architecture decomposition in drills/*/02-design-v1.md and verify clear component boundaries and responsibilities against drills/*/01-requirements.md. Use when design v1 is created or edited and findings must be written to reviews/topic-review.md.
---

# Architecture Decomposition

## Inputs
- Changed file: `drills/*/02-design-v1.md`
- Context files:
- `${DRILL_DIR}/01-requirements.md`
- `${DRILL_DIR}/02-design-v1.md`

## Procedure
1. Resolve `DRILL_DIR`, `TOPIC`, `REVIEW_FILE` from changed file path.
2. Map each component to one primary responsibility.
3. Verify data and control flow has no ownership ambiguity.
4. Confirm every major requirement has an owning component.

## Output
- Update `REVIEW_FILE` section: `Architecture Findings`
- For each finding, include: `boundary issue`, `risk`, `proposed split/merge`

## Fail Gate
Mark as fail if one of the following is true.
- One component owns multiple unrelated responsibilities.
- Core requirement has no owning component.
- Data flow crosses boundaries without contract.
