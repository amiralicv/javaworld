---
type: stage
series: Spring Boot
topics: 9
tags: [spring-boot, roadmap]
---

# 🌱 Actuator & Production Readiness

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/06 - Configuration & Properties/00 - Overview|06 - Configuration & Properties]] · 🏠 [[03 - Spring Boot/00 - Overview|Spring Boot]] · ➡️ [[03 - Spring Boot/08 - Testing/00 - Overview|08 - Testing]]

> Stage 9: Spring Boot Actuator & production-readiness. Your Security roadmap's Stage 19.3 told you to lock these endpoints down. This stage explains what they actually are, so the lockdown makes sense as more than a rule to follow.

---

## Stage 9 — Spring Boot Actuator & production-readiness

- 📊 [[03 - Spring Boot/07 - Actuator & Production Readiness/9.1 What Actuator actually is|9.1 What Actuator actually is]] · `0/4`
- 🌱 [[03 - Spring Boot/07 - Actuator & Production Readiness/9.2 Exposure control|9.2 Exposure control]] · `0/5`
- 🌱 [[03 - Spring Boot/07 - Actuator & Production Readiness/9.3 Built-in endpoints tour|9.3 Built-in endpoints tour]] · `0/11`
- 📊 [[03 - Spring Boot/07 - Actuator & Production Readiness/9.4 Health indicators|9.4 Health indicators]] · `0/7`
- 📊 [[03 - Spring Boot/07 - Actuator & Production Readiness/9.5 Metrics and Micrometer|9.5 Metrics and Micrometer]] · `0/9`
- 🛰️ [[03 - Spring Boot/07 - Actuator & Production Readiness/9.6 Distributed tracing|9.6 Distributed tracing]] · `0/5`
- 📊 [[03 - Spring Boot/07 - Actuator & Production Readiness/9.7 Securing Actuator|9.7 Securing Actuator (tying back to the Security roadmap)]] · `0/4`
- 📊 [[03 - Spring Boot/07 - Actuator & Production Readiness/9.8 Custom Actuator endpoints|9.8 Custom Actuator endpoints]] · `0/4`
- 🌱 [[03 - Spring Boot/07 - Actuator & Production Readiness/9.9 Info contributors|9.9 Info contributors]] · `0/3`

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("03 - Spring Boot/07 - Actuator & Production Readiness")'
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
