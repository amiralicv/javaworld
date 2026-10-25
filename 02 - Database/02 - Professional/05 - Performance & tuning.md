---
type: topic
series: Database
stage: "02 - Professional"
status: todo
items: 22
created: 2026-09-28
tags: [database, topic]
---

# ⚡ P. Performance & tuning

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/02 - Professional/04 - Indexing, deeper|O. Indexing, deeper]] · 🔼 [[02 - Database/02 - Professional/00 - Overview|02 - Professional]] · ➡️ [[02 - Database/02 - Professional/06 - Partitioning & large data|Q. Partitioning & large data]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **169. `EXPLAIN (ANALYZE, BUFFERS, VERBOSE, FORMAT TEXT)`** — buffers show you actual I/O, which timing alone hides.
- [ ] **170. Reading a plan properly** — actual vs estimated rows, loops, the most expensive node, and where time is really spent.
- [ ] **171. Plan visualizers** — pev2 / explain.depesz. Use them until plans read naturally.
- [ ] **172. Planner statistics and `ANALYZE`** — the planner guesses from samples; stale statistics produce terrible plans.
- [ ] **173. Extended statistics (`CREATE STATISTICS`)** — for correlated columns the planner otherwise treats as independent.
- [ ] **174. Key configuration knobs** — `shared_buffers`, `work_mem`, `effective_cache_size`, `random_page_cost`, `max_connections`. Know what each affects before touching it.
- [ ] **175. `work_mem` and spilling to disk** — a sort or hash that does not fit goes to disk and gets slow.
- [ ] **176. `pg_stat_statements`** — find your actual worst queries by total time, not by feeling.
- [ ] **177. `pg_stat_activity`** — see what is running, what is blocked, and what is waiting.
- [ ] **178. Lock inspection** — `pg_locks`, blocking-tree queries, finding the blocker.
- [ ] **179. `auto_explain` and slow query logging.**
- [ ] **180. MVCC in practice** — an `UPDATE` writes a new row version; old versions stay until vacuumed. This explains bloat, and why "update-heavy table, no vacuum" ends badly.
- [ ] **181. VACUUM and autovacuum** — what they reclaim, why they matter, when the defaults are too lazy for your workload.
- [ ] **182. `VACUUM FULL`** — rewrites the table and takes an exclusive lock. Rarely the answer.
- [ ] **183. Table and index bloat** — how to measure it, what causes it.
- [ ] **184. TOAST** — how Postgres stores large values out-of-line, and why a wide `text` column can be cheaper than it looks.
- [ ] **185. HOT updates and `fillfactor`** — updating a non-indexed column can avoid touching indexes.
- [ ] **186. Connection pooling** — every connection is a process. Use HikariCP in the app, PgBouncer in front for many services; understand transaction vs session pooling modes.
- [ ] **187. Batching writes** — multi-row inserts, `COPY`, and why 10,000 single-row inserts is a network problem, not a database problem.
- [ ] **188. Query rewriting techniques** — pushing filters down, avoiding `OR` across columns (`UNION ALL` instead), avoiding functions on indexed columns.
- [ ] **189. Caching layers** — materialized views, summary tables, Redis; and cache invalidation as the actual hard part.
- [ ] **190. Benchmarking honestly** — realistic data volume, warm vs cold cache, repeat runs. Optimizing against 100 dev rows teaches you nothing.

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
