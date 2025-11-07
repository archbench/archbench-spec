# Checkout — Scenario Brief

## Overview
Transactional checkout pipeline handling cart submission, payment authorization, and order persistence. Mix of synchronous payment calls and durable writes drives latency.

## Workload
- Requests/sec: **900**
- p95 latency target: **200 ms**

## Success Criteria
1. Payment service SLA keeps the overall p95 under 200 ms.
2. Orders DB sustains 900 writes/sec with indexes on `user_id` and `status`.
3. Cache absorbs product/pricing reads so API CPU stays < 70% utilization.

## Architecture Notes
- API orchestrates payment call, writes to cache for quick order lookups, and persists to MySQL.
- Consider idempotency keys + queues for retry logic in later packs.
- Payments service is the main bottleneck; experiments include circuit breakers or async capture.
