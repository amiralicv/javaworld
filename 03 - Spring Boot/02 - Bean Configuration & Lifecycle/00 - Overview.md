---
type: stage
series: Spring Boot
topics: 13
tags: [spring-boot, roadmap]
---

# 🌱 Bean Configuration & Lifecycle

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/01 - IoC, DI & Container/00 - Overview|01 - IoC, DI & Container]] · 🏠 [[03 - Spring Boot/00 - Overview|Spring Boot]] · ➡️ [[03 - Spring Boot/03 - Spring AOP/00 - Overview|03 - Spring AOP]]

> Stages 3–4: Bean configuration in depth, and the full bean lifecycle & scopes.

---

## Stage 3 — Bean configuration in depth

- ⚙️ [[03 - Spring Boot/02 - Bean Configuration & Lifecycle/3.1 @Configuration classes|3.1 `@Configuration` classes]] · `0/6`
- 🧩 [[03 - Spring Boot/02 - Bean Configuration & Lifecycle/3.2 Bean naming and identity|3.2 Bean naming and identity]] · `0/5`
- 🤖 [[03 - Spring Boot/02 - Bean Configuration & Lifecycle/3.3 Conditional bean registration|3.3 Conditional bean registration]] · `0/9`
- 🛡️ [[03 - Spring Boot/02 - Bean Configuration & Lifecycle/3.4 Externalized value injection|3.4 Externalized value injection]] · `0/6`
- ⚙️ [[03 - Spring Boot/02 - Bean Configuration & Lifecycle/3.5 Bean definition profiles and environments|3.5 Bean definition profiles and environments]] · `0/6`
- ⚙️ [[03 - Spring Boot/02 - Bean Configuration & Lifecycle/3.6 Importing configuration|3.6 Importing configuration]] · `0/5`
- 🫘 [[03 - Spring Boot/02 - Bean Configuration & Lifecycle/3.7 Scripting-dynamic bean registration|3.7 Scripting/dynamic bean registration (awareness level)]] · `0/2`

---

## Stage 4 — Bean lifecycle & scopes

- 🫘 [[03 - Spring Boot/02 - Bean Configuration & Lifecycle/4.1 The full bean lifecycle, in exact order|4.1 The full bean lifecycle, in exact order]] · `0/12`
- 🫘 [[03 - Spring Boot/02 - Bean Configuration & Lifecycle/4.2 Bean scopes|4.2 Bean scopes]] · `0/9`
- 🫘 [[03 - Spring Boot/02 - Bean Configuration & Lifecycle/4.3 The singleton-injecting-prototype problem|4.3 The singleton-injecting-prototype problem]] · `0/5`
- 🧠 [[03 - Spring Boot/02 - Bean Configuration & Lifecycle/4.4 Aware interfaces|4.4 `Aware` interfaces (the full family, beyond 4.1.4)]] · `0/6`
- 🫘 [[03 - Spring Boot/02 - Bean Configuration & Lifecycle/4.5 Application context lifecycle events|4.5 Application context lifecycle events]] · `0/9`
- 🌱 [[03 - Spring Boot/02 - Bean Configuration & Lifecycle/4.6 Circular dependency resolution mechanics|4.6 Circular dependency resolution mechanics (the deeper cut)]] · `0/4`

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("03 - Spring Boot/02 - Bean Configuration & Lifecycle")'
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
