---
type: topic
series: Database
stage: "02 - Professional"
status: todo
items: 11
created: 2026-09-28
tags: [database, topic]
---

# 🧮 N. Views, functions, triggers

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/02 - Professional/02 - Postgres-specific data features|M. Postgres-specific data features]] · 🔼 [[02 - Database/02 - Professional/00 - Overview|02 - Professional]] · ➡️ [[02 - Database/02 - Professional/04 - Indexing, deeper|O. Indexing, deeper]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **146. Views** — a named query. No storage, no performance gain by itself.
- [ ] **147. Updatable views and `INSTEAD OF` triggers.**
- [ ] **148. Materialized views** — the result is stored; `REFRESH MATERIALIZED VIEW CONCURRENTLY` to avoid blocking readers. Good for expensive dashboards.
- [ ] **149. Functions in PL/pgSQL** — variables, control flow, `RETURNS TABLE`, exceptions.
- [ ] **150. Function volatility** — `IMMUTABLE`, `STABLE`, `VOLATILE`, and why it decides whether an expression index is even allowed.
- [ ] **151. Procedures vs functions** — procedures can manage transactions.
- [ ] **152. Triggers** — `BEFORE`/`AFTER`, row vs statement level, `NEW`/`OLD`.
- [ ] **153. Good trigger uses** — `updated_at`, audit tables, denormalized counters.
- [ ] **154. Bad trigger uses** — business logic hidden from your application code. [Likely] the most common cause of "why did this row change?" mysteries.
- [ ] **155. `LISTEN` / `NOTIFY`** — lightweight pub/sub from the database.
- [ ] **156. Row-level security (RLS)** — per-row access policies; the real tool for multi-tenant isolation.

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
