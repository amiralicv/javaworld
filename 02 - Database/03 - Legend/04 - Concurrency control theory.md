---
type: topic
series: Database
stage: "03 - Legend"
status: todo
items: 8
created: 2026-09-28
tags: [database, topic]
---

# 🔄 X. Concurrency control theory

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/03 - Legend/03 - Query planner & optimizer internals|W. Query planner & optimizer internals]] · 🔼 [[02 - Database/03 - Legend/00 - Overview|03 - Legend]] · ➡️ [[02 - Database/03 - Legend/05 - Distributed data|Y. Distributed data]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **268. Serializability** — conflict serializable vs view serializable.
- [ ] **269. Two-phase locking (2PL) and strict 2PL.**
- [ ] **270. Timestamp ordering and optimistic concurrency control.**
- [ ] **271. Snapshot isolation and write skew** — the anomaly that snapshot isolation does not prevent.
- [ ] **272. Serializable Snapshot Isolation (SSI)** — Postgres's true `SERIALIZABLE`, predicate locks, and serialization failures your app must retry.
- [ ] **273. Lock manager internals** — lock modes, the lock table, lightweight locks, spinlocks, `LWLock` contention.
- [ ] **274. Deadlock detection algorithms** — wait-for graphs.
- [ ] **275. Latch vs lock** — protecting memory structures versus protecting data.

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
