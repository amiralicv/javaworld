---
type: topic
series: Database
stage: "01 - Must Know"
status: todo
items: 11
created: 2026-09-28
tags: [database, topic]
---

# 🔄 H. Transactions & concurrency

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/01 - Must Know/07 - Writing data|G. Writing data]] · 🔼 [[02 - Database/01 - Must Know/00 - Overview|01 - Must Know]] · ➡️ [[02 - Database/01 - Must Know/09 - Indexes - this belongs in tier 1, not later|I. Indexes — this belongs in tier 1, not later]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **63. What a transaction is** — a unit of work that fully happens or fully does not.
- [ ] **64. `BEGIN` / `COMMIT` / `ROLLBACK` / `SAVEPOINT`.**
- [ ] **65. ACID** — atomicity, consistency, isolation, durability. Know what each one actually promises.
- [ ] **66. Read phenomena** — dirty read, non-repeatable read, phantom read, lost update.
- [ ] **67. Isolation levels** — Read Uncommitted, Read Committed, Repeatable Read, Serializable, and which phenomena each prevents.
- [ ] **68. Postgres specifics** — the default is Read Committed; Postgres has no true Read Uncommitted; Repeatable Read is snapshot isolation.
- [ ] **69. Row locks** — `SELECT ... FOR UPDATE`, `FOR NO KEY UPDATE`, `FOR SHARE`, and `SKIP LOCKED` for queue patterns.
- [ ] **70. Deadlocks** — why they happen, why consistent lock ordering prevents them, why the loser gets an error and must retry.
- [ ] **71. Optimistic vs pessimistic locking** — a version column vs an actual lock.
- [ ] **72. Long transactions are poison** — they hold locks, block VACUUM, and grow bloat. Never keep a transaction open across a network call or user think-time.
- [ ] **73. Autocommit** — every bare statement is its own transaction. Know what your driver does.

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
