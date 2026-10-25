---
type: topic
series: Database
stage: "02 - Professional"
status: todo
items: 9
created: 2026-09-28
tags: [database, topic]
---

# 🧩 S. Schema change without downtime

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/02 - Professional/07 - Operations you must understand as a developer|R. Operations you must understand as a developer]] · 🔼 [[02 - Database/02 - Professional/00 - Overview|02 - Professional]] · ➡️ [[02 - Database/02 - Professional/09 - Beyond a single Postgres|T. Beyond a single Postgres]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **210. Lock levels of `ALTER TABLE`** — some are instant, some rewrite the whole table and block everything. Know which is which before you deploy.
- [ ] **211. Adding a column safely** — nullable or with a constant default is fast in modern Postgres; a volatile default rewrites the table.
- [ ] **212. Adding `NOT NULL` safely** — add a `CHECK ... NOT VALID`, validate, then convert.
- [ ] **213. Adding a constraint or foreign key with `NOT VALID` + `VALIDATE`.**
- [ ] **214. Renaming and dropping columns** — the expand/contract (parallel change) pattern across releases.
- [ ] **215. Backfilling large tables** — batched updates with sleeps, never one giant transaction.
- [ ] **216. `lock_timeout` and `statement_timeout` in migrations** — fail fast instead of blocking your whole application.
- [ ] **217. Blue/green and backwards-compatible schema** — the app version before and after must both work against the schema.
- [ ] **218. Migration tooling discipline** — forward-only, one change per migration, reviewed, tested against a production-sized copy.

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
