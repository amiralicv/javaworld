---
type: stage
series: Spring Data JPA
topics: 10
tags: [spring-data-jpa, roadmap]
---

# 💾 JDBC & Connection Pooling

> [!abstract] 🧭 Navigation
> ⬅️ [[04 - Spring Data JPA/02 - Advanced SQL & Indexing/00 - Overview|02 - Advanced SQL & Indexing]] · 🏠 [[04 - Spring Data JPA/00 - Overview|Spring Data JPA]] · ➡️ [[04 - Spring Data JPA/04 - ORM Theory & Hibernate Architecture/00 - Overview|04 - ORM Theory & Hibernate Architecture]]

> Stages 6–7: JDBC fundamentals, connection pooling. This is the layer Hibernate sits on top of — understanding it makes every later "why is Hibernate doing this" question answerable.

---

## Stage 6 — JDBC fundamentals

- 🔌 [[04 - Spring Data JPA/03 - JDBC & Connection Pooling/6.1 JDBC core concepts|6.1 JDBC core concepts]] · `0/13`
- 🔄 [[04 - Spring Data JPA/03 - JDBC & Connection Pooling/6.2 Transactions at the JDBC level|6.2 Transactions at the JDBC level]] · `0/5`
- 🚦 [[04 - Spring Data JPA/03 - JDBC & Connection Pooling/6.3 Batch operations|6.3 Batch operations]] · `0/4`
- 💾 [[04 - Spring Data JPA/03 - JDBC & Connection Pooling/6.4 Metadata and introspection|6.4 Metadata and introspection]] · `0/3`
- 🔌 [[04 - Spring Data JPA/03 - JDBC & Connection Pooling/6.5 Spring's JDBC abstraction|6.5 Spring's JDBC abstraction (below JPA, above raw JDBC)]] · `0/7`

---

## Stage 7 — Connection pooling

- 🔌 [[04 - Spring Data JPA/03 - JDBC & Connection Pooling/7.1 Why pooling exists|7.1 Why pooling exists]] · `0/4`
- 💾 [[04 - Spring Data JPA/03 - JDBC & Connection Pooling/7.2 HikariCP|7.2 HikariCP (Spring Boot's default)]] · `0/9`
- 🧩 [[04 - Spring Data JPA/03 - JDBC & Connection Pooling/7.3 Pool sizing and the thread-pool relationship|7.3 Pool sizing and the thread-pool relationship]] · `0/5`
- 💾 [[04 - Spring Data JPA/03 - JDBC & Connection Pooling/7.4 Multiple data sources|7.4 Multiple data sources]] · `0/4`
- 🚦 [[04 - Spring Data JPA/03 - JDBC & Connection Pooling/7.5 Operational awareness|7.5 Operational awareness]] · `0/4`

---

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("04 - Spring Data JPA/03 - JDBC & Connection Pooling")'
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
