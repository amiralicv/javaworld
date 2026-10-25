---
type: topic
series: Database
stage: "03 - Legend"
status: todo
items: 8
created: 2026-09-28
tags: [database, topic]
---

# 💽 V. Durability, recovery, WAL

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/03 - Legend/01 - Postgres storage internals|U. Postgres storage internals]] · 🔼 [[02 - Database/03 - Legend/00 - Overview|03 - Legend]] · ➡️ [[02 - Database/03 - Legend/03 - Query planner & optimizer internals|W. Query planner & optimizer internals]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **248. WAL record structure and LSNs.**
- [ ] **249. Full-page writes and torn-page protection.**
- [ ] **250. Checkpoint mechanics and tuning** — `max_wal_size`, `checkpoint_completion_target`.
- [ ] **251. Crash recovery / REDO** — how Postgres replays WAL on start.
- [ ] **252. ARIES recovery algorithm** — the classic paper behind most of this.
- [ ] **253. `fsync`, `synchronous_commit`, and honest durability trade-offs.**
- [ ] **254. Logical decoding** — turning physical WAL into logical change events; output plugins, replication slots and the disk they can eat.
- [ ] **255. Two-phase commit (`PREPARE TRANSACTION`)** — and why it is rarely used in practice.

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
