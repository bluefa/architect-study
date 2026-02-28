---
name: requirement-validation
description: Validate system design requirement docs under drills/*/01-requirements.md for completeness, measurable constraints, and contradictions. Use when requirement files are created or edited and a review update must be written to reviews/topic-review.md.
---

# Requirement Validation

## Inputs
- Changed file: `drills/*/01-requirements.md`
- Context file: same file only

## Procedure
1. Derive output path from changed file.
- `DRILL_DIR = dirname(changed_file)`
- `TOPIC = basename(DRILL_DIR)`
- `REVIEW_FILE = reviews/${TOPIC}-review.md`
2. Validate required sections.
- Goals vs non-goals are separated.
- Traffic/capacity assumptions are numeric.
- SLA/SLO include metric + target + window.
- Consistency level and RPO/RTO are defined.
- Open questions contain at least 3 items.
3. Detect contradiction.
- Non-goals do not conflict with goals.
- SLO does not conflict with traffic assumptions.

## Output
- Update `REVIEW_FILE` section: `Requirements Findings`
- Record each issue with: `problem`, `impact`, `fix suggestion`

## Fail Gate
Mark as fail if one of the following is true.
- SLO is not measurable.
- Non-goal section is missing.
- Consistency model is undefined.
- Open questions are fewer than 3.
