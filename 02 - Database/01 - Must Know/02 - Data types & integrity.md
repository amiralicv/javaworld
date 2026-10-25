---
type: topic
series: Database
stage: "01 - Must Know"
status: todo
items: 14
created: 2026-09-28
tags: [database, topic]
---

# 🧱 B. Data types & integrity

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/01 - Must Know/01 - What a database actually is|A. What a database actually is]] · 🔼 [[02 - Database/01 - Must Know/00 - Overview|01 - Must Know]] · ➡️ [[02 - Database/01 - Must Know/03 - Core SQL - reading data|C. Core SQL — reading data]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **8. Numeric types** — `smallint`, `integer`, `bigint`, `numeric/decimal`, `real/double`. Money is `numeric`, never floating point.
- [ ] **9. Text types** — `text`, `varchar(n)`, `char(n)`. In Postgres `text` and `varchar` perform identically; `char(n)` pads with spaces and is a trap.
- [ ] **10. Boolean, and why a nullable boolean has three states.**
- [ ] **11. Date & time types** — `date`, `time`, `timestamp`, `timestamptz`, `interval`. Use `timestamptz` and store UTC.
- [ ] **12. UUID type** — real UUID column, not a string.
- [ ] **13. `json` vs `jsonb`** — `jsonb` is parsed, indexable and reorders keys; `json` keeps raw text. Use `jsonb`.
- [ ] **14. Arrays** — Postgres can store an array in a column. Convenient, but often a modelling shortcut you regret.
- [ ] **15. Enum types vs lookup tables** — enums are fast but painful to change; lookup tables are flexible.
- [ ] **16. NULL and three-valued logic** — `NULL = NULL` is not true, it is unknown. `NOT IN` with a NULL returns nothing. This single topic causes more silent wrong results than any other.
- [ ] **17. `IS NULL` / `IS NOT NULL` / `IS DISTINCT FROM`.**
- [ ] **18. Constraints: `NOT NULL`, `UNIQUE`, `CHECK`, `DEFAULT`** — push rules into the database. Application-only validation always leaks eventually.
- [ ] **19. Primary key** — unique + not null + the row's identity.
- [ ] **20. Foreign key** — referential integrity, plus `ON DELETE` / `ON UPDATE` actions (`CASCADE`, `RESTRICT`, `SET NULL`).
- [ ] **21. Why unique constraints beat "check first, then insert"** — the check-then-act pattern is a race condition. The constraint is the only real guarantee.

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
