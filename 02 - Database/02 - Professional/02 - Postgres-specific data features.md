---
type: topic
series: Database
stage: "02 - Professional"
status: todo
items: 15
created: 2026-09-28
tags: [database, topic]
---

# 🗄️ M. Postgres-specific data features

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/02 - Professional/01 - Advanced query writing|L. Advanced query writing]] · 🔼 [[02 - Database/02 - Professional/00 - Overview|02 - Professional]] · ➡️ [[02 - Database/02 - Professional/03 - Views, functions, triggers|N. Views, functions, triggers]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **131. JSONB operators** — `->`, `->>`, `#>`, `@>`, `?`, `jsonb_set`, `jsonb_build_object`.
- [ ] **132. JSONPath (`@?`, `jsonb_path_query`).**
- [ ] **133. Indexing JSONB** — GIN with `jsonb_ops` vs `jsonb_path_ops`, and expression indexes on a single key.
- [ ] **134. Array operators and indexing** — `@>`, `&&`, `ANY`, GIN indexes.
- [ ] **135. Full-text search** — `tsvector`, `tsquery`, `to_tsvector`, ranking, dictionaries, GIN index, generated tsvector columns.
- [ ] **136. Trigram search (`pg_trgm`)** — fuzzy matching and fast `LIKE '%x%'` with a GIN/GiST index.
- [ ] **137. Range types** — `int4range`, `tstzrange`, containment operators.
- [ ] **138. Exclusion constraints** — "no two bookings for this room may overlap", enforced by the database.
- [ ] **139. Composite types and domains** — custom types with constraints.
- [ ] **140. `hstore`** — the older key/value type; know it exists, prefer JSONB.
- [ ] **141. Generated columns** — stored computed columns.
- [ ] **142. Identity columns, sequences, and `setval` recovery.**
- [ ] **143. `COPY`** — bulk load, orders of magnitude faster than row-by-row inserts.
- [ ] **144. Foreign data wrappers (`postgres_fdw`, `file_fdw`)** — query another database or a CSV as if it were a table.
- [ ] **145. Extensions** — how to install them, and the ones worth knowing: `pg_trgm`, `pgcrypto`, `uuid-ossp`, `postgis`, `pg_stat_statements`, `citext`.

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
