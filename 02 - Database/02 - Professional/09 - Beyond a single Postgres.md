---
type: topic
series: Database
stage: "02 - Professional"
status: todo
items: 17
created: 2026-09-28
tags: [database, topic]
---

# 🧠 T. Beyond a single Postgres

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/02 - Professional/08 - Schema change without downtime|S. Schema change without downtime]] · 🔼 [[02 - Database/02 - Professional/00 - Overview|02 - Professional]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **219. OLTP vs OLAP** — different access patterns need different shapes and often different systems.
- [ ] **220. Star schema, facts and dimensions** — basic warehouse modelling.
- [ ] **221. Columnar stores** — ClickHouse, DuckDB, and why analytics belongs there rather than in your production OLTP database.
- [ ] **222. ETL / ELT basics** — extract, load, transform; dbt as the common tool.
- [ ] **223. Change data capture (CDC)** — logical decoding and Debezium; streaming database changes into Kafka.
- [ ] **224. Transactional outbox** — the correct way to publish an event and commit a row atomically.
- [ ] **225. Job queues in Postgres** — `SELECT ... FOR UPDATE SKIP LOCKED`; good enough far longer than people expect.
- [ ] **226. Sharding basics** — key choice, rebalancing, cross-shard queries, and why you delay it as long as possible.
- [ ] **227. Multi-tenancy strategies** — shared table with `tenant_id`, schema per tenant, database per tenant; and RLS as the enforcement layer.
- [ ] **228. Caching with Redis in front of Postgres** — patterns and invalidation.
- [ ] **229. Search engines** — when Postgres full-text stops being enough and Elasticsearch/OpenSearch starts earning its cost.
- [ ] **230. Other engines for comparison** — MySQL differences, SQLite for local/tests, MongoDB's model and its trade-offs.
- [ ] **231. Testing against real Postgres** — Testcontainers, seeded fixtures, migration tests. H2 lies about SQL.
- [ ] **232. Anonymized production-like data for testing.**
- [ ] **233. Query linting and review** — catching `SELECT *`, missing indexes and full scans before merge.
- [ ] **234. Cost awareness on managed services** — IOPS, storage growth, connection limits, egress.
- [ ] **235. Capacity planning** — growth per month, when your current instance stops being enough.

## 📝 My Notes

> [!note] ✍️ In your own words
> What is it? Why does it exist? When should you **not** use it?

## 💻 Code

```sql
// minimal working example
```

## ⚠️ Gotchas & Traps

-

## ❓ Self-Test

- [ ] I can explain this out loud in 2 minutes without notes
- [ ] I wrote working code for it without copying

## 🔗 Related

-
