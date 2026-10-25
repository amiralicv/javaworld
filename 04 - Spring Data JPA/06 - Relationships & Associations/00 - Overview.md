---
type: stage
series: Spring Data JPA
topics: 9
tags: [spring-data-jpa, roadmap]
---

# 💾 Relationships & Associations

> [!abstract] 🧭 Navigation
> ⬅️ [[04 - Spring Data JPA/05 - Entity Mapping/00 - Overview|05 - Entity Mapping]] · 🏠 [[04 - Spring Data JPA/00 - Overview|Spring Data JPA]] · ➡️ [[04 - Spring Data JPA/07 - Repositories & Queries/00 - Overview|07 - Repositories & Queries]]

> Stage 11: Relationships & associations. [Likely] more production bugs trace back to this single stage than to all others combined. Slow down here, especially on fetch types and cascade.

---

## Stage 11 — Relationships & associations

- 💾 [[04 - Spring Data JPA/06 - Relationships & Associations/11.1 Foundational concepts before any annotation|11.1 Foundational concepts before any annotation]] · `0/7`
- 💾 [[04 - Spring Data JPA/06 - Relationships & Associations/11.2 @ManyToOne|11.2 `@ManyToOne`]] · `0/6`
- 💾 [[04 - Spring Data JPA/06 - Relationships & Associations/11.3 @OneToMany|11.3 `@OneToMany`]] · `0/7`
- 💾 [[04 - Spring Data JPA/06 - Relationships & Associations/11.4 @OneToOne|11.4 `@OneToOne`]] · `0/5`
- 💾 [[04 - Spring Data JPA/06 - Relationships & Associations/11.5 @ManyToMany|11.5 `@ManyToMany`]] · `0/6`
- 💾 [[04 - Spring Data JPA/06 - Relationships & Associations/11.6 Cascade types|11.6 Cascade types]] · `0/10`
- ⚡ [[04 - Spring Data JPA/06 - Relationships & Associations/11.7 Fetch strategies in depth|11.7 Fetch strategies in depth]] · `0/8`
- 🧩 [[04 - Spring Data JPA/06 - Relationships & Associations/11.8 Bidirectional relationship management pitfalls|11.8 Bidirectional relationship management pitfalls]] · `0/4`
- 🧩 [[04 - Spring Data JPA/06 - Relationships & Associations/11.9 Modeling decisions and trade-offs|11.9 Modeling decisions and trade-offs]] · `0/4`

---

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("04 - Spring Data JPA/06 - Relationships & Associations")'
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
