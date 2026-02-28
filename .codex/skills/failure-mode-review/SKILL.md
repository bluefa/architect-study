---
name: failure-mode-review
description: Review failure modes for drills/*/02-design-v1.md and drills/*/04-design-v2.md, including SPOF, data loss, retry storms, and partial outages. Use when design or tradeoff files change and failure scenarios must be written to reviews/topic-review.md.
---

# Failure Mode Review

## Inputs
- Changed file: `drills/*/02-design-v1.md`, `drills/*/04-design-v2.md`, or `drills/*/03-tradeoffs.md`
- Context files:
- `${DRILL_DIR}/02-design-v1.md`
- `${DRILL_DIR}/03-tradeoffs.md`
- `${DRILL_DIR}/04-design-v2.md` (if exists)

## Procedure
1. Resolve `DRILL_DIR`, `TOPIC`, `REVIEW_FILE`.
2. Enumerate at least 3 failure scenarios.
3. For each scenario, define detection signal, mitigation, and recovery steps.
4. Highlight customer-facing impact and degraded-mode behavior.

## Output
- Update `REVIEW_FILE` section: `Failure Scenarios`
- Format each row as: `scenario | detection | mitigation | recovery`

## Fail Gate
Mark as fail if one of the following is true.
- Recovery steps are missing.
- Only normal-path behavior is described.
- Customer impact is unspecified.
