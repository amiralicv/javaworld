---
type: topic
series: Database
stage: "03 - Legend"
status: todo
items: 12
created: 2026-09-28
tags: [database, topic]
---

# 🔬 U. Postgres storage internals

> [!abstract] 🧭 Navigation
> 🔼 [[02 - Database/03 - Legend/00 - Overview|03 - Legend]] · ➡️ [[02 - Database/03 - Legend/02 - Durability, recovery, WAL|V. Durability, recovery, WAL]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **236. Physical layout** — cluster directory, tablespaces, relation files, 1 GB segments, the `pg_class` / `pg_attribute` catalogs.
- [ ] **237. Page structure** — the 8 KB page: header, item pointers, tuples, free space, special area.
- [ ] **238. Tuple headers** — `xmin`, `xmax`, `ctid`, infomask bits. Once you can read these, MVCC stops being abstract.
- [ ] **239. MVCC visibility rules** — how a snapshot decides which row versions you can see.
- [ ] **240. Snapshots and transaction IDs** — `xid`, running-transaction lists, `txid_current()`.
- [ ] **241. Transaction ID wraparound** — the 32-bit counter, freezing, aggressive vacuum, and the shutdown that saves your data.
- [ ] **242. Freeze maps and visibility maps** — what makes index-only scans and cheap vacuums possible.
- [ ] **243. Dead tuples, bloat mechanics, and free space maps.**
- [ ] **244. HOT chains in detail.**
- [ ] **245. TOAST internals** — compression, out-of-line storage, storage strategies (`PLAIN`, `EXTENDED`, `EXTERNAL`, `MAIN`).
- [ ] **246. Buffer manager** — shared buffers, pinning, the clock-sweep replacement algorithm, and the OS page cache underneath.
- [ ] **247. Background processes** — checkpointer, background writer, WAL writer, autovacuum launcher, stats collector.

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
