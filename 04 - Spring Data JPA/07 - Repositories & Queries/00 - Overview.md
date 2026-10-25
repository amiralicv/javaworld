---
type: stage
series: Spring Data JPA
topics: 13
tags: [spring-data-jpa, roadmap]
---

# 💾 Repositories & Queries

> [!abstract] 🧭 Navigation
> ⬅️ [[04 - Spring Data JPA/06 - Relationships & Associations/00 - Overview|06 - Relationships & Associations]] · 🏠 [[04 - Spring Data JPA/00 - Overview|Spring Data JPA]] · ➡️ [[04 - Spring Data JPA/08 - Performance & Transactions/00 - Overview|08 - Performance & Transactions]]

> Stages 12–13: Spring Data JPA repositories, queries. This is the layer most tutorials start at — you now have the foundation to understand _why_ it works, not just that it works.

---

## Stage 12 — Spring Data JPA repositories

- 📦 [[04 - Spring Data JPA/07 - Repositories & Queries/12.1 The repository abstraction|12.1 The repository abstraction]] · `0/10`
- 🎯 [[04 - Spring Data JPA/07 - Repositories & Queries/12.2 save semantics - the most misunderstood method|12.2 `save()` semantics — the most misunderstood method]] · `0/6`
- 🔍 [[04 - Spring Data JPA/07 - Repositories & Queries/12.3 Query derivation from method names|12.3 Query derivation from method names]] · `0/15`
- 🔍 [[04 - Spring Data JPA/07 - Repositories & Queries/12.4 @Query - explicit queries|12.4 `@Query` — explicit queries]] · `0/11`
- 🔍 [[04 - Spring Data JPA/07 - Repositories & Queries/12.5 Query by Example|12.5 Query by Example (QBE)]] · `0/5`
- 🗃️ [[04 - Spring Data JPA/07 - Repositories & Queries/12.6 JPA Criteria API and Specifications|12.6 JPA Criteria API and Specifications]] · `0/10`
- 📦 [[04 - Spring Data JPA/07 - Repositories & Queries/12.7 Custom repository implementations|12.7 Custom repository implementations]] · `0/7`
- 📦 [[04 - Spring Data JPA/07 - Repositories & Queries/12.8 Repository configuration details|12.8 Repository configuration details]] · `0/6`

---

## Stage 13 — Query languages: JPQL, native SQL, projections, pagination

- 🔍 [[04 - Spring Data JPA/07 - Repositories & Queries/13.1 JPQL|13.1 JPQL (Jakarta Persistence Query Language)]] · `0/12`
- 🔍 [[04 - Spring Data JPA/07 - Repositories & Queries/13.2 Native SQL queries|13.2 Native SQL queries]] · `0/8`
- ⚡ [[04 - Spring Data JPA/07 - Repositories & Queries/13.3 Projections|13.3 Projections (fetching less than the full entity)]] · `0/10`
- 💾 [[04 - Spring Data JPA/07 - Repositories & Queries/13.4 Pagination and sorting|13.4 Pagination and sorting]] · `0/9`
- 💾 [[04 - Spring Data JPA/07 - Repositories & Queries/13.5 Sorting and filtering combined patterns|13.5 Sorting and filtering combined patterns]] · `0/3`

---

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("04 - Spring Data JPA/07 - Repositories & Queries")'
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
