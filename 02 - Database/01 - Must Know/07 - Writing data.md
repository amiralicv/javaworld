---
type: topic
series: Database
stage: "01 - Must Know"
status: todo
items: 7
created: 2026-09-28
tags: [database, topic]
---

# 🗄️ G. Writing data

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/01 - Must Know/06 - Expressions & functions|F. Expressions & functions]] · 🔼 [[02 - Database/01 - Must Know/00 - Overview|01 - Must Know]] · ➡️ [[02 - Database/01 - Must Know/08 - Transactions & concurrency|H. Transactions & concurrency]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **56. `INSERT`** — single row, multi-row, `INSERT ... SELECT`.
- [ ] **57. `RETURNING`** — get the generated ID or the updated row back in the same statement. Postgres-specific and very useful.
- [ ] **58. `UPDATE`** — with `FROM` for update-from-another-table.
- [ ] **59. `DELETE`** — and `USING`.
- [ ] **60. `ON CONFLICT DO UPDATE / DO NOTHING` (upsert)** — the correct, race-free insert-or-update.
- [ ] **61. `TRUNCATE` vs `DELETE`** — speed, transactionality, sequence reset, foreign keys.
- [ ] **62. The safety habit** — run `SELECT` first, then wrap the write in an explicit transaction. [Certain] Everyone deletes a whole table exactly once; make it not be in production.

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
