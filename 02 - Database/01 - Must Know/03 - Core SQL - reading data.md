---
type: topic
series: Database
stage: "01 - Must Know"
status: todo
items: 10
created: 2026-09-28
tags: [database, topic]
---

# 🔍 C. Core SQL — reading data

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/01 - Must Know/02 - Data types & integrity|B. Data types & integrity]] · 🔼 [[02 - Database/01 - Must Know/00 - Overview|01 - Must Know]] · ➡️ [[02 - Database/01 - Must Know/04 - Joins|D. Joins]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **22. `SELECT`, column list, `*` and why `*` is bad in application code.**
- [ ] **23. `WHERE` and operators** — comparison, `BETWEEN`, `IN`, `LIKE`/`ILIKE`, `~` regex.
- [ ] **24. `ORDER BY`** — ascending/descending, `NULLS FIRST/LAST`, multiple keys.
- [ ] **25. `LIMIT` / `OFFSET`** — and the fact that `LIMIT` without `ORDER BY` returns an arbitrary row.
- [ ] **26. `DISTINCT`.**
- [ ] **27. Aliases (`AS`) and table aliases.**
- [ ] **28. Aggregate functions** — `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`, and how each treats NULL. `COUNT(*)` vs `COUNT(col)` differ.
- [ ] **29. `GROUP BY`** — one output row per group; every selected column must be grouped or aggregated.
- [ ] **30. `HAVING`** — filter after grouping, unlike `WHERE`.
- [ ] **31. Logical order of execution** — `FROM` → `JOIN` → `WHERE` → `GROUP BY` → `HAVING` → `SELECT` → `DISTINCT` → `ORDER BY` → `LIMIT`. Learn this and half of SQL's "weird rules" become obvious (for example, why you cannot use a `SELECT` alias in `WHERE`).

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
