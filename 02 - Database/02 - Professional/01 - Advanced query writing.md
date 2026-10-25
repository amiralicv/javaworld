---
type: topic
series: Database
stage: "02 - Professional"
status: todo
items: 20
created: 2026-09-28
tags: [database, topic]
---

# 🔍 L. Advanced query writing

> [!abstract] 🧭 Navigation
> 🔼 [[02 - Database/02 - Professional/00 - Overview|02 - Professional]] · ➡️ [[02 - Database/02 - Professional/02 - Postgres-specific data features|M. Postgres-specific data features]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **111. CTEs (`WITH`)** — name a subquery, read the query top-to-bottom. Note: in modern Postgres a CTE is inlined by default, but `MATERIALIZED` / `NOT MATERIALIZED` lets you force it.
- [ ] **112. Recursive CTEs** — trees, hierarchies, graph walks, generated sequences.
- [ ] **113. Window functions — the concept** — aggregate *without* collapsing rows. The biggest single jump in SQL power.
- [ ] **114. `ROW_NUMBER`, `RANK`, `DENSE_RANK`, `NTILE`.**
- [ ] **115. `LAG` / `LEAD`** — compare a row with the previous or next one (deltas, gaps, session detection).
- [ ] **116. `SUM/AVG/COUNT ... OVER (PARTITION BY ... ORDER BY ...)`** — running totals and moving averages.
- [ ] **117. Window frames** — `ROWS` vs `RANGE`, `UNBOUNDED PRECEDING`, `CURRENT ROW`. The default frame surprises people.
- [ ] **118. `FIRST_VALUE`, `LAST_VALUE`, `NTH_VALUE`.**
- [ ] **119. `DISTINCT ON`** — Postgres shortcut for "the latest row per group".
- [ ] **120. `FILTER (WHERE ...)`** — conditional aggregates, cleaner than `CASE` inside `SUM`.
- [ ] **121. `GROUPING SETS`, `ROLLUP`, `CUBE`** — several levels of aggregation in one pass.
- [ ] **122. `LATERAL` joins** — a subquery that can reference the row on its left. Top-N-per-group, correlated expansion.
- [ ] **123. Set-returning functions** — `generate_series`, `unnest`, `jsonb_array_elements`.
- [ ] **124. `VALUES` lists as inline tables.**
- [ ] **125. Data-modifying CTEs** — `WITH deleted AS (DELETE ... RETURNING ...) INSERT ...` for atomic move/archive.
- [ ] **126. `MERGE`** — the SQL-standard multi-action upsert (Postgres 15+).
- [ ] **127. Anti-joins and semi-joins** — `NOT EXISTS` versus `LEFT JOIN ... WHERE ... IS NULL`, and their NULL behaviour.
- [ ] **128. Pivot / unpivot patterns** — with `FILTER`, `crosstab`, or `unnest`.
- [ ] **129. Gaps-and-islands problems** — the classic window-function exercise.
- [ ] **130. Query readability** — CTE naming, formatting, and knowing when a 200-line query should become a view.

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
