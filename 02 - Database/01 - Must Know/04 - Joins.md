---
type: topic
series: Database
stage: "01 - Must Know"
status: todo
items: 9
created: 2026-09-28
tags: [database, topic]
---

# 🔗 D. Joins

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/01 - Must Know/03 - Core SQL - reading data|C. Core SQL — reading data]] · 🔼 [[02 - Database/01 - Must Know/00 - Overview|01 - Must Know]] · ➡️ [[02 - Database/01 - Must Know/05 - Subqueries & set operations|E. Subqueries & set operations]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **32. `INNER JOIN`** — only matching rows.
- [ ] **33. `LEFT JOIN`** — keep all left rows, NULL-fill the right.
- [ ] **34. `RIGHT JOIN` / `FULL OUTER JOIN`.**
- [ ] **35. `CROSS JOIN`** — every combination; usually an accident.
- [ ] **36. The `LEFT JOIN` + `WHERE` trap** — putting a right-table condition in `WHERE` silently turns your outer join into an inner join. Put it in `ON` instead.
- [ ] **37. Self join** — a table joined to itself (hierarchies, comparisons).
- [ ] **38. Joining on multiple columns / composite keys.**
- [ ] **39. Join and row multiplication** — a one-to-many join multiplies rows and quietly corrupts your `SUM`. Aggregate before joining, or use a subquery.
- [ ] **40. `USING` and `NATURAL JOIN`** — shortcuts; `NATURAL JOIN` is dangerous because it depends on column names.

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
