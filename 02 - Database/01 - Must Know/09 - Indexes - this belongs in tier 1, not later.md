---
type: topic
series: Database
stage: "01 - Must Know"
status: todo
items: 14
created: 2026-09-28
tags: [database, topic]
---

# 📇 I. Indexes — this belongs in tier 1, not later

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/01 - Must Know/08 - Transactions & concurrency|H. Transactions & concurrency]] · 🔼 [[02 - Database/01 - Must Know/00 - Overview|01 - Must Know]] · ➡️ [[02 - Database/01 - Must Know/10 - Data modelling|J. Data modelling]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **74. What an index is** — a separate, ordered structure that turns a full scan into a targeted lookup. Default type: B-tree.
- [ ] **75. The trade** — faster reads, slower writes, more disk. Indexes are not free.
- [ ] **76. Primary key and unique constraints create indexes automatically.**
- [ ] **77. Foreign keys do NOT create an index in Postgres** — a very common cause of slow joins and slow deletes. Add it yourself.
- [ ] **78. Composite index and column order** — the leftmost-prefix rule decides which queries can use it. `(a, b)` helps `WHERE a`, not `WHERE b`.
- [ ] **79. Selectivity / cardinality** — an index on a column with 2 distinct values usually will not be used.
- [ ] **80. When an index is ignored** — a function or cast on the column (`WHERE lower(email) = ...`), leading wildcard `LIKE '%x'`, type mismatch, or the planner deciding a seq scan is cheaper.
- [ ] **81. Index-only scan / covering index** — when the index alone answers the query, the table is never touched.
- [ ] **82. `EXPLAIN` and `EXPLAIN ANALYZE`** 🔴 — the single most valuable database skill. `EXPLAIN` shows the plan; `ANALYZE` actually runs it and shows real times and row counts.
- [ ] **83. Reading a plan** — read inner nodes first; compare *estimated* rows with *actual* rows. A large gap means the planner is misinformed, and that is usually the real problem.
- [ ] **84. Scan types** — sequential scan, index scan, index-only scan, bitmap heap scan, and when each is correct. A seq scan is not automatically bad.
- [ ] **85. Join strategies** — nested loop, hash join, merge join, and which one fits which data size.
- [ ] **86. Pagination performance** — `OFFSET 100000` reads and discards 100,000 rows. Use keyset ("seek") pagination: `WHERE (created_at, id) < (?, ?) ORDER BY ... LIMIT n`.
- [ ] **87. `COUNT(*)` on a big table is slow** — and why exact totals in a paginated UI are often not worth the price.

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
