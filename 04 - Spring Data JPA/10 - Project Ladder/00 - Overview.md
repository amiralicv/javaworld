---
type: stage
series: Spring Data JPA
topics: 6
tags: [spring-data-jpa, roadmap]
---

# 💾 Project Ladder

> [!abstract] 🧭 Navigation
> ⬅️ [[04 - Spring Data JPA/09 - Auditing, Migrations & Testing/00 - Overview|09 - Auditing, Migrations & Testing]] · 🏠 [[04 - Spring Data JPA/00 - Overview|Spring Data JPA]]

> Stage 18: Project ladder. Same principle as the Security roadmap — reading 17 stages gives you vocabulary, these 5 projects force actual muscle memory. Do them **in order**.

---

## Stage 18 — Project ladder

- 🔍 [[04 - Spring Data JPA/10 - Project Ladder/18.1 Project 1 - Schema design + raw SQL mastery|18.1 Project 1 — Schema design + raw SQL mastery (Stages 1–3 applied, no JPA yet)]] · `0/7`
- 🗃️ [[04 - Spring Data JPA/10 - Project Ladder/18.2 Project 2 - First real Spring Data JPA CRUD app|18.2 Project 2 — First real Spring Data JPA CRUD app (Stages 8–13 applied)]] · `0/9`
- ⚡ [[04 - Spring Data JPA/10 - Project Ladder/18.3 Project 3 - Performance-hardened API|18.3 Project 3 — Performance-hardened API (Stages 14–15 applied)]] · `0/9`
- 🏗️ [[04 - Spring Data JPA/10 - Project Ladder/18.4 Project 4 - Multi-tenant, audited, migration-driven system|18.4 Project 4 — Multi-tenant, audited, migration-driven system (Stages 16 applied)]] · `0/6`
- 🏗️ [[04 - Spring Data JPA/10 - Project Ladder/18.5 Project 5 - Production-grade capstone|18.5 Project 5 — Production-grade capstone (Stage 17 + everything integrated)]] · `0/8`
- 💾 [[04 - Spring Data JPA/10 - Project Ladder/01 - You are done when|You are done when...]] · `0/4`

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("04 - Spring Data JPA/10 - Project Ladder")'
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
