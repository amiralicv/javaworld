---
type: topic
series: Database
stage: "01 - Must Know"
status: todo
items: 7
created: 2026-09-28
tags: [database, topic]
---

# 🗄️ A. What a database actually is

> [!abstract] 🧭 Navigation
> 🔼 [[02 - Database/01 - Must Know/00 - Overview|01 - Must Know]] · ➡️ [[02 - Database/01 - Must Know/02 - Data types & integrity|B. Data types & integrity]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **1. Database vs file storage** — concurrency, durability, querying and integrity are the four things a file cannot give you.
- [ ] **2. RDBMS vs NoSQL** — relational is the default; NoSQL is a trade you make for a specific reason (scale shape, schema flexibility), not a fashion.
- [ ] **3. Client / server model** — your app talks to a separate process over TCP. Every query is a network round trip.
- [ ] **4. Table, row (tuple), column (attribute)** — plus the mental model: a table is a set, not a list. There is no natural order.
- [ ] **5. Schema** — the namespace inside a database. In Postgres: cluster → database → schema → table.
- [ ] **6. SQL sub-languages** — DDL (create/alter), DML (insert/update/delete), DQL (select), TCL (commit/rollback), DCL (grant/revoke).
- [ ] **7. Declarative thinking** — you describe *what* you want; the planner decides *how*. This is why the same result can be 1ms or 10s.

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
