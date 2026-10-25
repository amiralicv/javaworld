---
type: topic
series: Spring Data JPA
stage: "01 - Database Theory, SQL & ACID"
status: todo
items: 20
created: 2026-09-28
tags: [spring-data-jpa, topic]
---

# 🔄 Stage 3 — Transactions and ACID

> [!abstract] 🧭 Navigation
> ⬅️ [[04 - Spring Data JPA/01 - Database Theory, SQL & ACID/2.7 Conditional and utility expressions|2.7 Conditional and utility expressions]] · 🔼 [[04 - Spring Data JPA/01 - Database Theory, SQL & ACID/00 - Overview|01 - Database Theory, SQL & ACID]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] 3.1 What a transaction is — a unit of work that succeeds or fails as a whole
- [ ] 3.2 **A**tomicity — all or nothing
- [ ] 3.3 **C**onsistency — the database moves between valid states only
- [ ] 3.4 **I**solation — concurrent transactions don't corrupt each other's view
- [ ] 3.5 **D**urability — once committed, it survives a crash
- [ ] 3.6 `BEGIN`/`START TRANSACTION`, `COMMIT`, `ROLLBACK`
- [ ] 3.7 Savepoints — partial rollback within a transaction
- [ ] 3.8 Isolation levels: `READ UNCOMMITTED`, `READ COMMITTED`, `REPEATABLE READ`, `SERIALIZABLE`
- [ ] 3.9 Dirty read, non-repeatable read, phantom read — which isolation level prevents which
- [ ] 3.10 Default isolation level per vendor (Postgres: Read Committed, MySQL/InnoDB: Repeatable Read) — and why assuming they match is a bug source
- [ ] 3.11 Locking: shared (read) lock vs exclusive (write) lock
- [ ] 3.12 Pessimistic locking — `SELECT ... FOR UPDATE`
- [ ] 3.13 Optimistic locking — version column, compare-and-swap on update
- [ ] 3.14 Deadlocks — how they happen, how the database detects and breaks them
- [ ] 3.15 Lock granularity: row-level vs table-level vs page-level
- [ ] 3.16 MVCC (Multi-Version Concurrency Control) — how Postgres/MySQL avoid read locks blocking writes
- [ ] 3.17 The lost update problem and which isolation level/locking strategy prevents it
- [ ] 3.18 Write skew — a subtle anomaly `SERIALIZABLE` alone doesn't always catch without care
- [ ] 3.19 Distributed transactions concept: two-phase commit (2PC) — and why it's usually avoided in modern microservices
- [ ] 3.20 Eventual consistency and the Saga pattern as the microservices-era alternative

## 📝 My Notes

> [!note] ✍️ In your own words
> What is it? Why does it exist? When should you **not** use it?

## 💻 Code

```java
// minimal working example
```

## ⚠️ Gotchas & Traps

-

## ❓ Self-Test

- [ ] I can explain this out loud in 2 minutes without notes
- [ ] I wrote working code for it without copying

## 🔗 Related

-
