---
type: stage
series: Spring Boot
topics: 9
tags: [spring-boot, roadmap]
---

# 🌱 Spring AOP

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/02 - Bean Configuration & Lifecycle/00 - Overview|02 - Bean Configuration & Lifecycle]] · 🏠 [[03 - Spring Boot/00 - Overview|Spring Boot]] · ➡️ [[03 - Spring Boot/04 - Spring MVC & Web Layer/00 - Overview|04 - Spring MVC & Web Layer]]

> Stage 5: Spring AOP. This is the stage that finally explains the "magic" from both your Security and JPA roadmaps — `@Transactional`, `@PreAuthorize`, and `@Cacheable` are not framework mysticism, they're all the same proxy mechanism applied to different advice logic.

---

## Stage 5 — Spring AOP

- 🪄 [[03 - Spring Boot/03 - Spring AOP/5.1 Why AOP exists|5.1 Why AOP exists]] · `0/4`
- 🪄 [[03 - Spring Boot/03 - Spring AOP/5.2 Spring AOP vs full AspectJ|5.2 Spring AOP vs full AspectJ]] · `0/5`
- 🪄 [[03 - Spring Boot/03 - Spring AOP/5.3 How the proxy is actually built|5.3 How the proxy is actually built]] · `0/8`
- 🪄 [[03 - Spring Boot/03 - Spring AOP/5.4 Advice types|5.4 Advice types]] · `0/8`
- 🪄 [[03 - Spring Boot/03 - Spring AOP/5.5 Pointcut expressions|5.5 Pointcut expressions]] · `0/11`
- 🪄 [[03 - Spring Boot/03 - Spring AOP/5.6 Declaring aspects|5.6 Declaring aspects]] · `0/5`
- 🌱 [[03 - Spring Boot/03 - Spring AOP/5.7 Where this connects to everything you've already learned|5.7 Where this connects to everything you've already learned]] · `0/6`
- 🪄 [[03 - Spring Boot/03 - Spring AOP/5.8 Writing your own aspect|5.8 Writing your own aspect (the exercise that cements this)]] · `0/4`
- ⚡ [[03 - Spring Boot/03 - Spring AOP/5.9 AOP performance and debugging|5.9 AOP performance and debugging]] · `0/3`

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("03 - Spring Boot/03 - Spring AOP")'
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
