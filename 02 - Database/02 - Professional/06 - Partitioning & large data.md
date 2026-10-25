---
type: topic
series: Database
stage: "02 - Professional"
status: todo
items: 7
created: 2026-09-28
tags: [database, topic]
---

# 🛰️ Q. Partitioning & large data

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/02 - Professional/05 - Performance & tuning|P. Performance & tuning]] · 🔼 [[02 - Database/02 - Professional/00 - Overview|02 - Professional]] · ➡️ [[02 - Database/02 - Professional/07 - Operations you must understand as a developer|R. Operations you must understand as a developer]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **191. Declarative partitioning** — range, list, hash.
- [ ] **192. Partition pruning** — the whole point; it only works if your query filters on the partition key.
- [ ] **193. Partition maintenance** — creating future partitions, detaching and archiving old ones, `pg_partman`.
- [ ] **194. When partitioning does NOT help** — under roughly tens of millions of rows, a good index is usually the better answer.
- [ ] **195. Time-series patterns** — BRIN plus range partitions, retention policies, TimescaleDB as an option.
- [ ] **196. Archiving and retention** — moving cold data out instead of letting the table grow forever.
- [ ] **197. Bulk delete strategies** — batched deletes, or partition detach instead of `DELETE`.

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
