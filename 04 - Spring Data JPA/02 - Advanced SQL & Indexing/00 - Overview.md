---
type: stage
series: Spring Data JPA
topics: 11
tags: [spring-data-jpa, roadmap]
---

# 💾 Advanced SQL & Indexing

> [!abstract] 🧭 Navigation
> ⬅️ [[04 - Spring Data JPA/01 - Database Theory, SQL & ACID/00 - Overview|01 - Database Theory, SQL & ACID]] · 🏠 [[04 - Spring Data JPA/00 - Overview|Spring Data JPA]] · ➡️ [[04 - Spring Data JPA/03 - JDBC & Connection Pooling/00 - Overview|03 - JDBC & Connection Pooling]]

> Stages 4–5: Advanced SQL, indexing & query performance.

---

## Stage 4 — Advanced SQL

- 🧮 [[04 - Spring Data JPA/02 - Advanced SQL & Indexing/4.1 Views and materialized views|4.1 Views and materialized views]] · `0/5`
- 🧮 [[04 - Spring Data JPA/02 - Advanced SQL & Indexing/4.2 Stored procedures and functions|4.2 Stored procedures and functions]] · `0/5`
- 🧩 [[04 - Spring Data JPA/02 - Advanced SQL & Indexing/4.3 Sequences and identity generation|4.3 Sequences and identity generation]] · `0/6`
- 🧱 [[04 - Spring Data JPA/02 - Advanced SQL & Indexing/4.4 Advanced constraints and data integrity|4.4 Advanced constraints and data integrity]] · `0/4`
- 💾 [[04 - Spring Data JPA/02 - Advanced SQL & Indexing/4.5 JSON and semi-structured data in relational databases|4.5 JSON and semi-structured data in relational databases]] · `0/5`
- 🛰️ [[04 - Spring Data JPA/02 - Advanced SQL & Indexing/4.6 Partitioning and large-table strategies|4.6 Partitioning and large-table strategies]] · `0/5`

---

## Stage 5 — Indexing and query performance

- 📇 [[04 - Spring Data JPA/02 - Advanced SQL & Indexing/5.1 Index fundamentals|5.1 Index fundamentals]] · `0/11`
- 📇 [[04 - Spring Data JPA/02 - Advanced SQL & Indexing/5.2 When indexes hurt|5.2 When indexes hurt]] · `0/4`
- 🔍 [[04 - Spring Data JPA/02 - Advanced SQL & Indexing/5.3 Reading query plans|5.3 Reading query plans]] · `0/8`
- ⚡ [[04 - Spring Data JPA/02 - Advanced SQL & Indexing/5.4 Common performance killers|5.4 Common performance killers (and their fixes)]] · `0/10`
- ⚡ [[04 - Spring Data JPA/02 - Advanced SQL & Indexing/5.5 Connection and query-level tuning basics|5.5 Connection and query-level tuning basics]] · `0/6`

---

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("04 - Spring Data JPA/02 - Advanced SQL & Indexing")'
    - 'note.type == "topic"'
formulas:
  state: 'if(note.status == "done", "✅ done", if(note.status == "learning", "🟨 learning", "⬜ todo"))'
views:
  - type: table
    name: 📊 Progress
    order:
      - file.name
      - formula.state
      - note.items
    sort:
      - property: file.name
        direction: ASC
```
