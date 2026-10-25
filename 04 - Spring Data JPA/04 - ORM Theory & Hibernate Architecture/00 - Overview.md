---
type: stage
series: Spring Data JPA
topics: 11
tags: [spring-data-jpa, roadmap]
---

# 💾 ORM Theory & Hibernate Architecture

> [!abstract] 🧭 Navigation
> ⬅️ [[04 - Spring Data JPA/03 - JDBC & Connection Pooling/00 - Overview|03 - JDBC & Connection Pooling]] · 🏠 [[04 - Spring Data JPA/00 - Overview|Spring Data JPA]] · ➡️ [[04 - Spring Data JPA/05 - Entity Mapping/00 - Overview|05 - Entity Mapping]]

> Stages 8–9: JPA specification & ORM theory, Hibernate architecture. This is where "Spring Data JPA" actually starts — everything before this was the foundation it stands on.

---

## Stage 8 — ORM theory and the JPA specification

- 💾 [[04 - Spring Data JPA/04 - ORM Theory & Hibernate Architecture/8.1 The object-relational impedance mismatch|8.1 The object-relational impedance mismatch]] · `0/5`
- 🗃️ [[04 - Spring Data JPA/04 - ORM Theory & Hibernate Architecture/8.2 JPA as a specification vs Hibernate as an implementation|8.2 JPA as a specification vs Hibernate as an implementation]] · `0/6`
- 🗃️ [[04 - Spring Data JPA/04 - ORM Theory & Hibernate Architecture/8.3 Core JPA concepts|8.3 Core JPA concepts]] · `0/6`
- 🧩 [[04 - Spring Data JPA/04 - ORM Theory & Hibernate Architecture/8.4 Entity lifecycle states|8.4 Entity lifecycle states]] · `0/11`
- 💾 [[04 - Spring Data JPA/04 - ORM Theory & Hibernate Architecture/8.5 The persistence context in depth|8.5 The persistence context in depth]] · `0/9`
- 🫘 [[04 - Spring Data JPA/04 - ORM Theory & Hibernate Architecture/8.6 Persistence context scope patterns|8.6 Persistence context scope patterns]] · `0/6`

---

## Stage 9 — Hibernate architecture

- 💾 [[04 - Spring Data JPA/04 - ORM Theory & Hibernate Architecture/9.1 Bootstrapping|9.1 Bootstrapping]] · `0/6`
- ⚙️ [[04 - Spring Data JPA/04 - ORM Theory & Hibernate Architecture/9.2 Configuration properties that matter|9.2 Configuration properties that matter]] · `0/8`
- 🧩 [[04 - Spring Data JPA/04 - ORM Theory & Hibernate Architecture/9.3 Schema generation and validation|9.3 Schema generation and validation]] · `0/4`
- 🗃️ [[04 - Spring Data JPA/04 - ORM Theory & Hibernate Architecture/9.4 The Hibernate type system|9.4 The Hibernate type system]] · `0/7`
- 🔍 [[04 - Spring Data JPA/04 - ORM Theory & Hibernate Architecture/9.5 SQL generation dialects and abstraction leaks|9.5 SQL generation dialects and abstraction leaks]] · `0/4`

---

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("04 - Spring Data JPA/04 - ORM Theory & Hibernate Architecture")'
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
