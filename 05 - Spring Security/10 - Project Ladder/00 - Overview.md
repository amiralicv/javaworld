---
type: stage
series: Spring Security
topics: 6
tags: [spring-security, roadmap]
---

# 🔐 Project Ladder

> [!abstract] 🧭 Navigation
> ⬅️ [[05 - Spring Security/09 - Production Hardening/00 - Overview|09 - Production Hardening]] · 🏠 [[05 - Spring Security/00 - Overview|Spring Security]]

> Stage 20: Project ladder. Reading the first 19 stages gives you vocabulary, not skill. These 5 projects force you to actually wire it together, break it, and fix it. Do them **in order** — each assumes the previous one's muscle memory.

---

## Stage 20 — Project ladder

- 🍪 [[05 - Spring Security/10 - Project Ladder/20.1 Project 1 - Classic session-based web app|20.1 Project 1 — Classic session-based web app (Stages 0–12 applied)]] · `0/10`
- 🎟️ [[05 - Spring Security/10 - Project Ladder/20.2 Project 2 - Stateless JWT REST API|20.2 Project 2 — Stateless JWT REST API (Stages 13 applied)]] · `0/8`
- 🌐 [[05 - Spring Security/10 - Project Ladder/20.3 Project 3 - Social login + first-party API|20.3 Project 3 — Social login + first-party API (Stage 14 applied)]] · `0/7`
- 🏗️ [[05 - Spring Security/10 - Project Ladder/20.4 Project 4 - Multi-service system with a real Authorization Server|20.4 Project 4 — Multi-service system with a real Authorization Server (Stages 14.5, 16, 18.2 applied)]] · `0/8`
- 🏗️ [[05 - Spring Security/10 - Project Ladder/20.5 Project 5 - Production-hardened capstone|20.5 Project 5 — Production-hardened capstone (Stage 19 applied, everything integrated)]] · `0/10`
- 🔐 [[05 - Spring Security/10 - Project Ladder/01 - You are done when|You are done when...]] · `0/4`

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("05 - Spring Security/10 - Project Ladder")'
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
