---
type: stage
series: Spring Boot
topics: 7
tags: [spring-boot, roadmap]
---

# 🌱 Configuration & Properties

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/05 - Auto-Configuration Internals/00 - Overview|05 - Auto-Configuration Internals]] · 🏠 [[03 - Spring Boot/00 - Overview|Spring Boot]] · ➡️ [[03 - Spring Boot/07 - Actuator & Production Readiness/00 - Overview|07 - Actuator & Production Readiness]]

> Stage 8: Spring Boot configuration & properties. This stage takes `@Value` (Stage 3.4) and profiles (Stage 3.5) further — into the structured, type-safe, environment-driven configuration model Boot actually expects you to use at scale.

---

## Stage 8 — Spring Boot configuration & properties

- ⚙️ [[03 - Spring Boot/06 - Configuration & Properties/8.1 Property file formats and structure|8.1 Property file formats and structure]] · `0/6`
- ⚙️ [[03 - Spring Boot/06 - Configuration & Properties/8.2 @ConfigurationProperties in full depth|8.2 `@ConfigurationProperties` in full depth]] · `0/9`
- ⚙️ [[03 - Spring Boot/06 - Configuration & Properties/8.3 Property source precedence|8.3 Property source precedence]] · `0/7`
- ⚙️ [[03 - Spring Boot/06 - Configuration & Properties/8.4 Profiles at the Boot application level|8.4 Profiles at the Boot application level (building on Stage 3.5)]] · `0/5`
- 🚦 [[03 - Spring Boot/06 - Configuration & Properties/8.5 Externalizing secrets properly|8.5 Externalizing secrets properly (bridging to production reality)]] · `0/4`
- ⚙️ [[03 - Spring Boot/06 - Configuration & Properties/8.6 Environment and property resolution APIs|8.6 `Environment` and property resolution APIs]] · `0/4`
- 🌱 [[03 - Spring Boot/06 - Configuration & Properties/8.7 Custom SpringApplication behavior|8.7 Custom `SpringApplication` behavior]] · `0/4`

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("03 - Spring Boot/06 - Configuration & Properties")'
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
