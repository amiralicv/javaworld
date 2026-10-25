---
type: stage
series: Spring Boot
topics: 6
tags: [spring-boot, roadmap]
---

# 🌱 Project Ladder

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/08 - Testing/00 - Overview|08 - Testing]] · 🏠 [[03 - Spring Boot/00 - Overview|Spring Boot]]

> Stage 11: Project ladder. Same principle as your other two roadmaps — these force the muscle memory the first 10 stages only gave you vocabulary for. Do them **in order**.

---

## Stage 11 — Project ladder

- 🏗️ [[03 - Spring Boot/09 - Project Ladder/11.1 Project 1 - Plain Spring, no Boot at all|11.1 Project 1 — Plain Spring, no Boot at all (Stages 1–4 applied)]] · `0/8`
- 🪄 [[03 - Spring Boot/09 - Project Ladder/11.2 Project 2 - AOP from scratch|11.2 Project 2 — AOP from scratch (Stage 5 applied)]] · `0/7`
- 🌐 [[03 - Spring Boot/09 - Project Ladder/11.3 Project 3 - Full Spring MVC REST API|11.3 Project 3 — Full Spring MVC REST API (Stage 6 applied)]] · `0/7`
- 🤖 [[03 - Spring Boot/09 - Project Ladder/11.4 Project 4 - Auto-configuration and properties from scratch|11.4 Project 4 — Auto-configuration and properties from scratch (Stages 7–8 applied)]] · `0/7`
- 🏗️ [[03 - Spring Boot/09 - Project Ladder/11.5 Project 5 - Production-instrumented capstone|11.5 Project 5 — Production-instrumented capstone (Stages 9–10 applied, everything integrated)]] · `0/9`
- 🌱 [[03 - Spring Boot/09 - Project Ladder/01 - You are done when|You are done when...]] · `0/4`

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("03 - Spring Boot/09 - Project Ladder")'
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
