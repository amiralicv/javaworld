---
type: stage
series: Spring Data JPA
topics: 11
tags: [spring-data-jpa, roadmap]
---

# 💾 Auditing, Migrations & Testing

> [!abstract] 🧭 Navigation
> ⬅️ [[04 - Spring Data JPA/08 - Performance & Transactions/00 - Overview|08 - Performance & Transactions]] · 🏠 [[04 - Spring Data JPA/00 - Overview|Spring Data JPA]] · ➡️ [[04 - Spring Data JPA/10 - Project Ladder/00 - Overview|10 - Project Ladder]]

> Stages 16–17: Auditing, migrations, multi-tenancy, and testing. Prerequisite: Stages 14–15. This part is about running real, evolving, shared databases safely — not just querying a static schema.

---

## Stage 16 — Auditing, schema migrations, and multi-tenancy

- 🗃️ [[04 - Spring Data JPA/09 - Auditing, Migrations & Testing/16.1 Spring Data JPA auditing|16.1 Spring Data JPA auditing]] · `0/9`
- 🧭 [[04 - Spring Data JPA/09 - Auditing, Migrations & Testing/16.2 Full history auditing|16.2 Full history auditing (beyond just "last modified")]] · `0/8`
- 🧩 [[04 - Spring Data JPA/09 - Auditing, Migrations & Testing/16.3 Schema migration tools|16.3 Schema migration tools]] · `0/9`
- 🧭 [[04 - Spring Data JPA/09 - Auditing, Migrations & Testing/16.4 Writing safe migrations|16.4 Writing safe migrations]] · `0/6`
- 🗃️ [[04 - Spring Data JPA/09 - Auditing, Migrations & Testing/16.5 Multi-tenancy with Spring Data JPA|16.5 Multi-tenancy with Spring Data JPA]] · `0/10`

---

## Stage 17 — Testing Spring Data JPA

- 🧪 [[04 - Spring Data JPA/09 - Auditing, Migrations & Testing/17.1 Test types and what each actually verifies|17.1 Test types and what each actually verifies]] · `0/6`
- 🧪 [[04 - Spring Data JPA/09 - Auditing, Migrations & Testing/17.2 Why in-memory databases are a testing trap|17.2 Why in-memory databases (H2) are a testing trap]] · `0/5`
- 🧪 [[04 - Spring Data JPA/09 - Auditing, Migrations & Testing/17.3 Testcontainers - testing against the real database engine|17.3 Testcontainers — testing against the real database engine]] · `0/8`
- 🧪 [[04 - Spring Data JPA/09 - Auditing, Migrations & Testing/17.4 What to actually test at the repository-persistence layer|17.4 What to actually test at the repository/persistence layer]] · `0/9`
- 🧪 [[04 - Spring Data JPA/09 - Auditing, Migrations & Testing/17.5 Test data setup patterns|17.5 Test data setup patterns]] · `0/5`
- 💾 [[04 - Spring Data JPA/09 - Auditing, Migrations & Testing/17.6 Assertions and tooling|17.6 Assertions and tooling]] · `0/3`

---

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("04 - Spring Data JPA/09 - Auditing, Migrations & Testing")'
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
