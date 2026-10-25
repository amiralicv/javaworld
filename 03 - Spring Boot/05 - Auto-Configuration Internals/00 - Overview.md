---
type: stage
series: Spring Boot
topics: 8
tags: [spring-boot, roadmap]
---

# 🌱 Auto-Configuration Internals

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/04 - Spring MVC & Web Layer/00 - Overview|04 - Spring MVC & Web Layer]] · 🏠 [[03 - Spring Boot/00 - Overview|Spring Boot]] · ➡️ [[03 - Spring Boot/06 - Configuration & Properties/00 - Overview|06 - Configuration & Properties]]

> Stage 7: Spring Boot auto-configuration internals. Everything before this stage was "how Spring works." This stage is specifically "how Spring **Boot** decides what to configure for you without being asked" — the exact mechanism your Security roadmap kept gesturing at (`spring-boot-starter-security` "does auto-configuration") without opening it up.

---

## Stage 7 — Spring Boot auto-configuration internals

- 🌱 [[03 - Spring Boot/05 - Auto-Configuration Internals/7.1 @SpringBootApplication unpacked|7.1 `@SpringBootApplication` unpacked]] · `0/5`
- ⚙️ [[03 - Spring Boot/05 - Auto-Configuration Internals/7.2 How @EnableAutoConfiguration actually finds configuration classes|7.2 How `@EnableAutoConfiguration` actually finds configuration classes]] · `0/5`
- 🤖 [[03 - Spring Boot/05 - Auto-Configuration Internals/7.3 Conditional evaluation in practice|7.3 Conditional evaluation in practice]] · `0/7`
- 🤖 [[03 - Spring Boot/05 - Auto-Configuration Internals/7.4 Starters vs auto-configuration - the distinction people conflate|7.4 Starters vs auto-configuration — the distinction people conflate]] · `0/4`
- 🤖 [[03 - Spring Boot/05 - Auto-Configuration Internals/7.5 Configuration properties feeding auto-configuration|7.5 Configuration properties feeding auto-configuration]] · `0/2`
- 🤖 [[03 - Spring Boot/05 - Auto-Configuration Internals/7.6 Embedded server auto-configuration as a concrete worked example|7.6 Embedded server auto-configuration as a concrete worked example]] · `0/3`
- 🤖 [[03 - Spring Boot/05 - Auto-Configuration Internals/7.7 Writing your own starter-auto-configuration|7.7 Writing your own starter/auto-configuration (the exercise that cements this stage)]] · `0/5`
- 🌱 [[03 - Spring Boot/05 - Auto-Configuration Internals/7.8 Failure analysis and startup diagnostics|7.8 Failure analysis and startup diagnostics]] · `0/3`

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("03 - Spring Boot/05 - Auto-Configuration Internals")'
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
