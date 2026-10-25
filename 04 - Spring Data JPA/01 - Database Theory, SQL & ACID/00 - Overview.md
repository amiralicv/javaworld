---
type: stage
series: Spring Data JPA
topics: 10
tags: [spring-data-jpa, roadmap]
---

# 💾 Database Theory, SQL & ACID

> [!abstract] 🧭 Navigation
> 🏠 [[04 - Spring Data JPA/00 - Overview|Spring Data JPA]] · ➡️ [[04 - Spring Data JPA/02 - Advanced SQL & Indexing/00 - Overview|02 - Advanced SQL & Indexing]]

> **How to use:** Tick `- [ ]` when you can explain the concept out loud and write code using it without copying.

---

- 📚 [[04 - Spring Data JPA/01 - Database Theory, SQL & ACID/Stage 0 - Prerequisites|Stage 0 — Prerequisites]] · `0/7`
- 📚 [[04 - Spring Data JPA/01 - Database Theory, SQL & ACID/Stage 1 - Relational database theory|Stage 1 — Relational database theory (do not skip)]] · `1/19`

---

## Stage 2 — SQL fundamentals

- 💾 [[04 - Spring Data JPA/01 - Database Theory, SQL & ACID/2.1 DDL|2.1 DDL (Data Definition Language)]] · `0/5`
- 💾 [[04 - Spring Data JPA/01 - Database Theory, SQL & ACID/2.2 DML|2.2 DML (Data Manipulation Language)]] · `0/5`
- 💾 [[04 - Spring Data JPA/01 - Database Theory, SQL & ACID/2.3 DQL|2.3 DQL (queries)]] · `0/9`
- 🔗 [[04 - Spring Data JPA/01 - Database Theory, SQL & ACID/2.4 Joins|2.4 Joins]] · `0/9`
- 🔍 [[04 - Spring Data JPA/01 - Database Theory, SQL & ACID/2.5 Subqueries and set operations|2.5 Subqueries and set operations]] · `0/9`
- 🧮 [[04 - Spring Data JPA/01 - Database Theory, SQL & ACID/2.6 Window functions|2.6 Window functions]] · `0/7`
- 🤖 [[04 - Spring Data JPA/01 - Database Theory, SQL & ACID/2.7 Conditional and utility expressions|2.7 Conditional and utility expressions]] · `0/6`
- 🔄 [[04 - Spring Data JPA/01 - Database Theory, SQL & ACID/Stage 3 - Transactions and ACID|Stage 3 — Transactions and ACID]] · `0/20`

---

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("04 - Spring Data JPA/01 - Database Theory, SQL & ACID")'
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
