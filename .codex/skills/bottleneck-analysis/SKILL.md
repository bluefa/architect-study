---
name: bottleneck-analysis
description: Analyze likely bottlenecks in drills/*/02-design-v1.md or drills/*/04-design-v2.md across read/write paths, storage, cache, and queue. Use when design files change and bottleneck findings must be updated in reviews/topic-review.md.
---

# Bottleneck Analysis

## Inputs
- Changed file: `drills/*/02-design-v1.md` or `drills/*/04-design-v2.md`
- Context files:
- `${DRILL_DIR}/01-requirements.md`
- `${DRILL_DIR}/02-design-v1.md`
- `${DRILL_DIR}/04-design-v2.md` (if exists)

## Procedure
1. Resolve `DRILL_DIR`, `TOPIC`, `REVIEW_FILE`.
2. Trace critical write path and read path.
3. Identify throughput/latency chokepoints in compute, storage, cache, queue.
4. Attach a threshold assumption and mitigation for each bottleneck.

## Output
- Update `REVIEW_FILE` section: `Bottlenecks`
- Include at least 2 bottleneck entries with mitigation and tradeoff.

## Fail Gate
Mark as fail if one of the following is true.
- Fewer than 2 concrete bottleneck candidates.
- No mitigation strategy per bottleneck.
- No threshold/trigger condition.
