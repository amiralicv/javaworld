---
type: stage
series: Spring Boot
topics: 8
tags: [spring-boot, roadmap]
---

# 🌱 IoC, DI & Container

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · 🏠 [[03 - Spring Boot/00 - Overview|Spring Boot]] · ➡️ [[03 - Spring Boot/02 - Bean Configuration & Lifecycle/00 - Overview|02 - Bean Configuration & Lifecycle]]

> Covers **Spring Framework Core + Spring Boot internals** — IoC/DI, bean lifecycle, AOP, Spring MVC, Boot auto-configuration, configuration, Actuator and testing. Spring Security and Spring Data JPA live in their own tracks.

---

- 📚 [[03 - Spring Boot/01 - IoC, DI & Container/Stage 0 - Prerequisites|Stage 0 — Prerequisites]] · `0/8`

---

## Stage 1 — Inversion of Control & Dependency Injection theory

- 🌱 [[03 - Spring Boot/01 - IoC, DI & Container/1.1 The core idea|1.1 The core idea]] · `0/5`
- 🛡️ [[03 - Spring Boot/01 - IoC, DI & Container/1.2 Types of dependency injection|1.2 Types of dependency injection]] · `0/8`
- 🌱 [[03 - Spring Boot/01 - IoC, DI & Container/1.3 Coupling to an interface vs a concrete class|1.3 Coupling to an interface vs a concrete class]] · `0/3`

---

## Stage 2 — The Spring IoC container

- 🫘 [[03 - Spring Boot/01 - IoC, DI & Container/2.1 Core container concepts|2.1 Core container concepts]] · `0/6`
- 🫘 [[03 - Spring Boot/01 - IoC, DI & Container/2.2 Registering beans - three ways|2.2 Registering beans — three ways]] · `0/6`
- 🌱 [[03 - Spring Boot/01 - IoC, DI & Container/2.3 Dependency resolution mechanics|2.3 Dependency resolution mechanics]] · `0/10`
- 🫘 [[03 - Spring Boot/01 - IoC, DI & Container/2.4 The container's startup process at a glance|2.4 The container's startup process at a glance]] · `0/5`

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("03 - Spring Boot/01 - IoC, DI & Container")'
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
