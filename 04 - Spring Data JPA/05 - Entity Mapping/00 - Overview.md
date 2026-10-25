---
type: stage
series: Spring Data JPA
topics: 9
tags: [spring-data-jpa, roadmap]
---

# 💾 Entity Mapping

> [!abstract] 🧭 Navigation
> ⬅️ [[04 - Spring Data JPA/04 - ORM Theory & Hibernate Architecture/00 - Overview|04 - ORM Theory & Hibernate Architecture]] · 🏠 [[04 - Spring Data JPA/00 - Overview|Spring Data JPA]] · ➡️ [[04 - Spring Data JPA/06 - Relationships & Associations/00 - Overview|06 - Relationships & Associations]]

> Stage 10: Entity mapping deep dive. This is the stage people rush through and pay for later — a wrong mapping decision here causes bugs that show up weeks later in production, not at compile time.

---

## Stage 10 — Entity mapping deep dive

- 🧩 [[04 - Spring Data JPA/05 - Entity Mapping/10.1 Declaring an entity|10.1 Declaring an entity]] · `0/8`
- 💾 [[04 - Spring Data JPA/05 - Entity Mapping/10.2 Primary keys|10.2 Primary keys]] · `0/12`
- 🧩 [[04 - Spring Data JPA/05 - Entity Mapping/10.3 Basic column mapping|10.3 Basic column mapping]] · `0/6`
- 🧩 [[04 - Spring Data JPA/05 - Entity Mapping/10.4 Entity equality and identity|10.4 Entity equality and identity]] · `0/7`
- 🧩 [[04 - Spring Data JPA/05 - Entity Mapping/10.5 Inheritance mapping strategies|10.5 Inheritance mapping strategies]] · `0/10`
- 💾 [[04 - Spring Data JPA/05 - Entity Mapping/10.6 Embeddable - value types|10.6 Embeddable / value types]] · `0/6`
- 📚 [[04 - Spring Data JPA/05 - Entity Mapping/10.7 Element collections|10.7 Element collections (collections of basic/embeddable types)]] · `0/7`
- 🧭 [[04 - Spring Data JPA/05 - Entity Mapping/10.8 Auditing fields|10.8 Auditing fields (a preview, full auditing in Stage 16)]] · `0/3`
- 🧩 [[04 - Spring Data JPA/05 - Entity Mapping/10.9 Entity listeners and lifecycle callbacks|10.9 Entity listeners and lifecycle callbacks]] · `0/5`

---

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("04 - Spring Data JPA/05 - Entity Mapping")'
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
