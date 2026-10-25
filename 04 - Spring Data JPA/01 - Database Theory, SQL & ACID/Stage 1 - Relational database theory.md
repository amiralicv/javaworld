---
type: topic
series: Spring Data JPA
stage: "01 - Database Theory, SQL & ACID"
status: learning
items: 19
created: 2026-09-28
tags: [spring-data-jpa, topic]
---

# 📚 Stage 1 — Relational database theory (do not skip)

> [!abstract] 🧭 Navigation
> ⬅️ [[04 - Spring Data JPA/01 - Database Theory, SQL & ACID/Stage 0 - Prerequisites|Stage 0 — Prerequisites]] · 🔼 [[04 - Spring Data JPA/01 - Database Theory, SQL & ACID/00 - Overview|01 - Database Theory, SQL & ACID]] · ➡️ [[04 - Spring Data JPA/01 - Database Theory, SQL & ACID/2.1 DDL|2.1 DDL (Data Definition Language)]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [x] 1.1 What a relational database is — tables, rows, columns, relations
- [ ] 1.2 Primary key — uniqueness + non-null guarantee
- [ ] 1.3 Natural key vs surrogate key, and why surrogate keys usually win in practice
- [ ] 1.4 Foreign key — referential integrity between tables
- [ ] 1.5 Candidate key, composite key, alternate key
- [ ] 1.6 Entity-Relationship (ER) modeling: entities, attributes, relationships
- [ ] 1.7 Cardinality: one-to-one, one-to-many, many-to-many
- [ ] 1.8 Normalization — 1NF, 2NF, 3NF (know what each eliminates)
- [ ] 1.9 BCNF and when 3NF isn't enough
- [ ] 1.10 Denormalization — when and why you deliberately break normal form
- [ ] 1.11 Schema design trade-offs: normalized OLTP vs denormalized reporting/OLAP
- [ ] 1.12 Constraints: `NOT NULL`, `UNIQUE`, `CHECK`, `DEFAULT`
- [ ] 1.13 Referential actions: `ON DELETE CASCADE`, `SET NULL`, `RESTRICT`, `NO ACTION`
- [ ] 1.14 Data types: numeric precision, `VARCHAR` vs `TEXT`, date/time types, `BOOLEAN` quirks per vendor
- [ ] 1.15 NULL semantics — three-valued logic (`TRUE`/`FALSE`/`UNKNOWN`) and why `NULL = NULL` is not true
- [ ] 1.16 Relational Algebra basics: selection, projection, join, union — the theory SQL is built on
- [ ] 1.17 Database vendors overview: PostgreSQL, MySQL, Oracle, SQL Server — know the differences exist before pretending SQL is "portable"
- [ ] 1.18 NoSQL landscape awareness: document (MongoDB), key-value, wide-column, graph — and why JPA/Hibernate is not the right tool for them
- [ ] 1.19 CAP theorem at a high level — why NoSQL exists as a trade-off, not a replacement

## 📝 My Notes

> [!note] ✍️ In your own words
> What is it? Why does it exist? When should you **not** use it?

## 💻 Code

```java
// minimal working example
```

## ⚠️ Gotchas & Traps

-

## ❓ Self-Test

- [ ] I can explain this out loud in 2 minutes without notes
- [ ] I wrote working code for it without copying

## 🔗 Related

-
