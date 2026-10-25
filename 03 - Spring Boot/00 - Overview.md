---
type: hub
series: Spring Boot
tags: [spring-boot, moc]
---

# 🌱 Spring Boot

> [!abstract] 🧭 Navigation
> 🏠 [[00 - Home|Home]]

> [!info] 📖 What this track covers
> Spring Framework Core + Spring Boot internals — IoC/DI, bean lifecycle, AOP, Spring MVC, auto-configuration, configuration, Actuator, testing and a project ladder.

## 🗺️ Stages

| # | Stage | Roadmap stages | Topics |
|---|---|---|---|
| 00 | 🗺️ [[03 - Spring Boot/00 - Concept Map/00 - Overview\|Concept Map]] | — | 28 |
| 01 | 🫘 [[03 - Spring Boot/01 - IoC, DI & Container/00 - Overview\|IoC, DI & Container]] | 0–2 | 8 |
| 02 | ⚙️ [[03 - Spring Boot/02 - Bean Configuration & Lifecycle/00 - Overview\|Bean Configuration & Lifecycle]] | 3–4 | 13 |
| 03 | 🪄 [[03 - Spring Boot/03 - Spring AOP/00 - Overview\|Spring AOP]] | 5 | 9 |
| 04 | 🌐 [[03 - Spring Boot/04 - Spring MVC & Web Layer/00 - Overview\|Spring MVC & Web Layer]] | 6 | 10 |
| 05 | 🔬 [[03 - Spring Boot/05 - Auto-Configuration Internals/00 - Overview\|Auto-Configuration Internals]] | 7 | 8 |
| 06 | ⚙️ [[03 - Spring Boot/06 - Configuration & Properties/00 - Overview\|Configuration & Properties]] | 8 | 7 |
| 07 | 📊 [[03 - Spring Boot/07 - Actuator & Production Readiness/00 - Overview\|Actuator & Production Readiness]] | 9 | 9 |
| 08 | 🧪 [[03 - Spring Boot/08 - Testing/00 - Overview\|Testing]] | 10 | 11 |
| 09 | 🏗️ [[03 - Spring Boot/09 - Project Ladder/00 - Overview\|Project Ladder]] | 11 | 6 |

> [!tip] 🎯 How to work through it
> 1. Open a stage, then a topic note.
> 2. Learn → write **📝 My Notes** in your own words → write **💻 Code**.
> 3. Tick boxes only when you can explain them out loud. Update `status` as you go.

## 📊 Progress

```base
filters:
  and:
    - 'file.inFolder("03 - Spring Boot")'
    - 'note.type == "topic"'
formulas:
  state: 'if(note.status == "done", "✅ done", if(note.status == "learning", "🟨 learning", "⬜ todo"))'
views:
  - type: table
    name: 📊 Progress
    groupBy:
      property: note.stage
      direction: ASC
    order:
      - file.name
      - formula.state
      - note.items
    sort:
      - property: file.name
        direction: ASC
```
