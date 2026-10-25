---
type: topic
series: Database
stage: "01 - Must Know"
status: todo
items: 10
created: 2026-09-28
tags: [database, topic]
---

# 🗄️ K. Postgres in practice

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/01 - Must Know/10 - Data modelling|J. Data modelling]] · 🔼 [[02 - Database/01 - Must Know/00 - Overview|01 - Must Know]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **101. Running Postgres** — Docker for local, managed service for production.
- [ ] **102. `psql`** — connecting, and the meta-commands: `\l`, `\c`, `\dt`, `\d table`, `\di`, `\df`, `\x`, `\timing`.
- [ ] **103. Cluster → database → schema → table**, plus `search_path`.
- [ ] **104. Roles and privileges** — `CREATE ROLE`, `GRANT`, `REVOKE`, ownership, and least privilege for your app user.
- [ ] **105. Connection strings & SSL** — and connection limits, which are lower than you think.
- [ ] **106. A GUI client** — DBeaver or pgAdmin, for exploring and for `EXPLAIN` visualisation.
- [ ] **107. `pg_dump` / `pg_restore` / `psql < file`** — logical backup and restore basics.
- [ ] **108. Migrations as code** — Flyway or Liquibase; versioned, forward-only, reviewed. Never change schema by hand in production.
- [ ] **109. SQL injection & parameterized queries** 🔴 — string concatenation into SQL is the vulnerability. Bind parameters always, including in dynamic ORDER BY (validate against a whitelist).
- [ ] **110. Least privilege for the app user** — your API does not need `SUPERUSER` or `DROP TABLE`.

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
