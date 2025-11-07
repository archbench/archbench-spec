# URL Shortener — Scenario Brief

## Overview
Classic read-heavy service: clients hit an API to expand short codes. Hot paths are cache hits; cold paths perform a primary-key lookup in a relational DB.

## Workload
- Requests/sec: **1,800**
- p95 latency target: **150 ms**

## Success Criteria
1. Cache hit ratio keeps p95 under 150 ms even with DB latency spikes.
2. Database capacity supports at least 1,800 req/s without saturation.
3. Cost stays under \$0.50/hour for the baseline deployment.

## Architecture Notes
- Cache stores `{ short_code -> target_url }` with 1-hour TTL.
- Database indexes `short_code` and keeps metadata (created_at, owner).
- Adding write replicas or larger cache tiers is the go-to knob for experiments.
