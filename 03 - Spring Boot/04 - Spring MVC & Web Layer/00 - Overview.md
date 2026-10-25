---
type: stage
series: Spring Boot
topics: 10
tags: [spring-boot, roadmap]
---

# 🌱 Spring MVC & Web Layer

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/03 - Spring AOP/00 - Overview|03 - Spring AOP]] · 🏠 [[03 - Spring Boot/00 - Overview|Spring Boot]] · ➡️ [[03 - Spring Boot/05 - Auto-Configuration Internals/00 - Overview|05 - Auto-Configuration Internals]]

> Stage 6: Spring MVC & the web layer. This connects directly back to your Security roadmap's Stage 4 (servlet filters run _before_ this whole stage even begins).

---

## Stage 6 — Spring MVC & the web layer

- 🌐 [[03 - Spring Boot/04 - Spring MVC & Web Layer/6.1 The front controller pattern and DispatcherServlet|6.1 The front controller pattern and `DispatcherServlet`]] · `0/5`
- 🫘 [[03 - Spring Boot/04 - Spring MVC & Web Layer/6.2 The full request lifecycle, in exact order|6.2 The full request lifecycle, in exact order]] · `0/11`
- 🧩 [[03 - Spring Boot/04 - Spring MVC & Web Layer/6.3 Controllers and request mapping|6.3 Controllers and request mapping]] · `0/13`
- 🌐 [[03 - Spring Boot/04 - Spring MVC & Web Layer/6.4 HttpMessageConverter|6.4 `HttpMessageConverter`]] · `0/5`
- 🌱 [[03 - Spring Boot/04 - Spring MVC & Web Layer/6.5 Validation|6.5 Validation]] · `0/8`
- 🌱 [[03 - Spring Boot/04 - Spring MVC & Web Layer/6.6 Exception handling|6.6 Exception handling]] · `0/9`
- 🌐 [[03 - Spring Boot/04 - Spring MVC & Web Layer/6.7 Cross-cutting web concerns|6.7 Cross-cutting web concerns]] · `0/6`
- 🌱 [[03 - Spring Boot/04 - Spring MVC & Web Layer/6.8 File uploads and multipart handling|6.8 File uploads and multipart handling]] · `0/4`
- 🌐 [[03 - Spring Boot/04 - Spring MVC & Web Layer/6.9 WebClient and RestClient|6.9 WebClient and RestClient (calling other services)]] · `0/5`
- 🌀 [[03 - Spring Boot/04 - Spring MVC & Web Layer/6.10 Reactive web|6.10 Reactive web (bridge, not a repeat)]] · `0/2`

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("03 - Spring Boot/04 - Spring MVC & Web Layer")'
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
