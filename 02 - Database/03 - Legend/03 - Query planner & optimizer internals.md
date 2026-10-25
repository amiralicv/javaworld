---
type: topic
series: Database
stage: "03 - Legend"
status: todo
items: 12
created: 2026-09-28
tags: [database, topic]
---

# ⚡ W. Query planner & optimizer internals

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/03 - Legend/02 - Durability, recovery, WAL|V. Durability, recovery, WAL]] · 🔼 [[02 - Database/03 - Legend/00 - Overview|03 - Legend]] · ➡️ [[02 - Database/03 - Legend/04 - Concurrency control theory|X. Concurrency control theory]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **256. Parse → analyze → rewrite → plan → execute** — the five stages of a query.
- [ ] **257. Relational algebra** — selection, projection, join, and why the planner is allowed to reorder your query at all.
- [ ] **258. Cost model** — how `seq_page_cost`, `random_page_cost`, `cpu_tuple_cost` combine into a number.
- [ ] **259. Cardinality estimation** — the hardest problem in query optimization; errors compound multiplicatively up the plan tree.
- [ ] **260. Statistics internals** — histograms, most-common-values lists, `n_distinct`, correlation, and `default_statistics_target`.
- [ ] **261. Join order search** — dynamic programming, and GEQO (the genetic optimizer) for many-table joins.
- [ ] **262. Subquery flattening and predicate pushdown.**
- [ ] **263. Executor internals** — the volcano/iterator model, `ExecProcNode`.
- [ ] **264. Parallel query execution** — gather nodes, workers, what can and cannot be parallelized.
- [ ] **265. JIT compilation** — when it helps, and when it makes short queries slower.
- [ ] **266. Plan caching, prepared statements, generic vs custom plans** — the "it got slow after the 6th execution" mystery.
- [ ] **267. Hint-free philosophy** — why Postgres refuses query hints, and the tools you use instead (`pg_hint_plan`, statistics, rewriting).

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
