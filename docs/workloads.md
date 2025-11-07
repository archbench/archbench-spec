# ArchBench Workload Reference

Canonical workloads for the Training Pack scenarios. Use these numbers when creating presets or validating scenario JSON files.

| Scenario        | Requests/sec | p95 Target (ms) | Notes |
| --------------- | ------------ | --------------- | ----- |
| URL Shortener   | 1,800        | 150             | Heavy read traffic hitting cache first, write path goes to DB with secondary index. |
| Chat DM         | 2,500        | 120             | Gateway + queue absorbs bursty fan-out, worker writes into Mongo with compound indexes. |
| Checkout        | 900          | 200             | Payment hop plus DB writes dominate latency; cache fronts product/pricing reads. |

> Add new rows whenever a scenario JSON is added to `examples/`.
