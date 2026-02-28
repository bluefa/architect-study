---
name: cto-pressure-test
description: Pressure-test drills/*/04-design-v2.md and drills/*/05-adr-*.md under executive constraints (10x traffic, 50% budget, 2-week schedule cut). Use when v2 or ADR files change and risk/decision updates must be written to reviews/topic-review.md.
---

# CTO Pressure Test

## Inputs
- Changed file: `drills/*/04-design-v2.md` or `drills/*/05-adr-*.md`
- Context files:
- `${DRILL_DIR}/01-requirements.md`
- `${DRILL_DIR}/04-design-v2.md`
- `${DRILL_DIR}/05-adr-*.md`

## Procedure
1. Resolve `DRILL_DIR`, `TOPIC`, `REVIEW_FILE`.
2. Apply three pressure scenarios.
- Traffic x10
- Budget -50%
- Timeline -2 weeks
3. For each scenario, classify components into keep/defer/drop.
4. Check ADR consistency with the proposed scenario actions.

## Output
- Update `REVIEW_FILE` sections: `CTO Questions`, `Decision Risks`
- Add scenario-specific action list.

## Fail Gate
Mark as fail if one of the following is true.
- keep/defer/drop classification is missing for any scenario.
- ADR decisions and pressure response are inconsistent.
- No explicit risk acceptance or mitigation exists.
