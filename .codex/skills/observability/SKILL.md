---
name: observability
description: Review observability coverage for drills/*/02-design-v1.md and drills/*/04-design-v2.md including SLI, alerts, logs, metrics, tracing, and runbook links. Use when design docs change and observability actions must be written to reviews/topic-review.md.
---

# Observability

## Inputs
- Changed file: `drills/*/02-design-v1.md` or `drills/*/04-design-v2.md`
- Context files:
- `${DRILL_DIR}/01-requirements.md`
- `${DRILL_DIR}/02-design-v1.md`
- `${DRILL_DIR}/04-design-v2.md` (if exists)

## Procedure
1. Resolve `DRILL_DIR`, `TOPIC`, `REVIEW_FILE`.
2. Map each SLO to at least one measurable SLI.
3. Validate alert thresholds and paging conditions.
4. Check logs/metrics/traces and runbook availability.

## Output
- Update `REVIEW_FILE` section: `Observability`
- Add prioritized action items for missing signals or alerts.

## Fail Gate
Mark as fail if one of the following is true.
- SLI is not measurable.
- Alert threshold is undefined.
- No operational runbook path exists.
