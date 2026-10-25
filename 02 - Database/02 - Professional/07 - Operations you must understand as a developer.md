---
type: topic
series: Database
stage: "02 - Professional"
status: todo
items: 12
created: 2026-09-28
tags: [database, topic]
---

# 🚦 R. Operations you must understand as a developer

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/02 - Professional/06 - Partitioning & large data|Q. Partitioning & large data]] · 🔼 [[02 - Database/02 - Professional/00 - Overview|02 - Professional]] · ➡️ [[02 - Database/02 - Professional/08 - Schema change without downtime|S. Schema change without downtime]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **198. WAL (write-ahead log) — the concept** — changes are written to a log before the data files. This is what makes durability and replication possible.
- [ ] **199. Checkpoints** — and the I/O spikes they cause.
- [ ] **200. Logical vs physical backup** — `pg_dump` versus `pg_basebackup`.
- [ ] **201. Point-in-time recovery (PITR)** — base backup plus WAL archive.
- [ ] **202. Restore drills** — an untested backup is not a backup. [Certain]
- [ ] **203. Streaming replication** — primary/standby, synchronous vs asynchronous, replication lag.
- [ ] **204. Read replicas from the app side** — routing reads, and the fact that a replica can be stale (read-your-own-write problems).
- [ ] **205. Logical replication** — publications and subscriptions; replicate selected tables, or between versions.
- [ ] **206. Failover and HA** — Patroni, virtual IPs, what your application must do when the primary changes.
- [ ] **207. Major version upgrades** — `pg_upgrade` versus logical replication cutover.
- [ ] **208. Monitoring** — connections, cache hit ratio, replication lag, longest transaction, deadlocks, bloat, disk. Know the five you would alert on.
- [ ] **209. Security** — TLS, `pg_hba.conf`, role separation, column encryption with `pgcrypto`, secret management, audit logging.

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
