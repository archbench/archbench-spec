# Chat DM — Scenario Brief

## Overview
Direct-messaging service with gateway fan-in, durable queue buffering, and worker fleet persisting messages to a document store. Latency budget hinges on queue depth and worker throughput.

## Workload
- Requests/sec: **2,500**
- p95 latency target: **120 ms**

## Success Criteria
1. Queue depth remains < 200 messages at steady state.
2. Worker pool keeps end-to-end p95 under 120 ms, even during short spikes (1.2× nominal RPS).
3. Data store handles 2,500 writes/sec with indexes on `user_pair` and `created_at`.

## Architecture Notes
- Gateway authenticates and enqueues; workers pull, enrich, and insert into Mongo.
- Secondary indexes support inbox fetch; trade-offs revolve around shard count and index coverage.
- Consider cache tiers for presence data or fan-out read paths in future iterations.
