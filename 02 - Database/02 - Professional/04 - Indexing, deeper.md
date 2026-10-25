---
type: topic
series: Database
stage: "02 - Professional"
status: todo
items: 12
created: 2026-09-28
tags: [database, topic]
---

# 📇 O. Indexing, deeper

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/02 - Professional/03 - Views, functions, triggers|N. Views, functions, triggers]] · 🔼 [[02 - Database/02 - Professional/00 - Overview|02 - Professional]] · ➡️ [[02 - Database/02 - Professional/05 - Performance & tuning|P. Performance & tuning]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **157. Index types overview** — B-tree, Hash, GIN, GiST, SP-GiST, BRIN, and what data shape each is for.
- [ ] **158. GIN** — many values per row: arrays, JSONB, full text.
- [ ] **159. GiST** — geometry, ranges, nearest-neighbour.
- [ ] **160. BRIN** — tiny index for huge, naturally ordered tables (time-series).
- [ ] **161. Partial indexes** — `WHERE status = 'active'`; smaller and often dramatically faster.
- [ ] **162. Expression indexes** — `ON (lower(email))`, matching the exact expression your query uses.
- [ ] **163. Covering indexes with `INCLUDE`.**
- [ ] **164. `CREATE INDEX CONCURRENTLY`** — build an index without locking writes. Mandatory in production, and it can fail and leave an invalid index.
- [ ] **165. Operator classes and collations** — including `text_pattern_ops` for `LIKE 'abc%'`.
- [ ] **166. Unique partial indexes** — "only one active record per user".
- [ ] **167. Finding unused and duplicate indexes** — `pg_stat_user_indexes`. Unused indexes cost writes forever.
- [ ] **168. Index bloat and `REINDEX CONCURRENTLY`.**

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
