---
type: topic
series: Database
stage: "01 - Must Know"
status: todo
items: 7
created: 2026-09-28
tags: [database, topic]
---

# 🔍 E. Subqueries & set operations

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/01 - Must Know/04 - Joins|D. Joins]] · 🔼 [[02 - Database/01 - Must Know/00 - Overview|01 - Must Know]] · ➡️ [[02 - Database/01 - Must Know/06 - Expressions & functions|F. Expressions & functions]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **41. Scalar subquery** — one value inside `SELECT` or `WHERE`.
- [ ] **42. Subquery in `FROM` (derived table).**
- [ ] **43. Correlated subquery** — runs per row; know it because it explains many slow queries.
- [ ] **44. `IN` vs `EXISTS` vs `JOIN`** — semantics differ with NULLs and duplicates, not just performance.
- [ ] **45. `ANY` / `ALL`.**
- [ ] **46. `UNION` vs `UNION ALL`** — `UNION` deduplicates and costs a sort. Default to `UNION ALL` unless you need dedup.
- [ ] **47. `INTERSECT` / `EXCEPT`.**

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
