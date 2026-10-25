---
tags: [spring, springboot, java, roadmap]
status: in-progress
type: stage
series: Spring Boot
topics: 28
---

# 🗺️ Spring & Spring Boot — Complete Concept Map

> [!abstract] 🧭 Navigation
> 🏠 [[03 - Spring Boot/00 - Overview|Spring Boot]] · ➡️ [[03 - Spring Boot/01 - IoC, DI & Container/00 - Overview|01 - IoC, DI & Container]]

**How to use this in Obsidian:** each numbered line is one concept = one future note. Tick the box only after you can explain it out loud _and_ you have written code that uses it. When a concept gets big, turn it into its own note and link it back here.

Legend: 🔴 = you cannot skip this · 🟡 = important, learn after the basics · 🟢 = specialist / optional

---

- 📚 [[03 - Spring Boot/00 - Concept Map/Phase 00 - Prerequisites|Phase 0 — Prerequisites (Spring will feel like magic without these)]] · `0/10`
- 🫘 [[03 - Spring Boot/00 - Concept Map/Phase 01 - The IoC Container|Phase 1 — The IoC Container (the true core of Spring)]] · `0/23`
- 🫘 [[03 - Spring Boot/00 - Concept Map/Phase 02 - Bean Lifecycle, Scope, Extension Points|Phase 2 — Bean Lifecycle, Scope, Extension Points]] · `0/19`
- ⚙️ [[03 - Spring Boot/00 - Concept Map/Phase 03 - Configuration & Environment|Phase 3 — Configuration & Environment]] · `0/17`
- 🪄 [[03 - Spring Boot/00 - Concept Map/Phase 04 - AOP|Phase 4 — AOP (Aspect-Oriented Programming)]] · `0/11`
- 📚 [[03 - Spring Boot/00 - Concept Map/Phase 05 - Spring Boot Fundamentals|Phase 5 — Spring Boot Fundamentals]] · `0/16`
- 🌐 [[03 - Spring Boot/00 - Concept Map/Phase 06 - Spring MVC & Building REST APIs|Phase 6 — Spring MVC & Building REST APIs]] · `0/26`
- 🌐 [[03 - Spring Boot/00 - Concept Map/Phase 07 - Calling Other Services|Phase 7 — Calling Other Services (HTTP clients)]] · `0/6`
- 🔄 [[03 - Spring Boot/00 - Concept Map/Phase 08 - Data Access & Transactions|Phase 8 — Data Access & Transactions]] · `0/36`
- 🧪 [[03 - Spring Boot/00 - Concept Map/Phase 09 - Testing|Phase 9 — Testing (learn this earlier than you want to)]] · `0/16`
- 🌱 [[03 - Spring Boot/00 - Concept Map/Phase 10 - Spring Security|Phase 10 — Spring Security]] · `0/21`
- 📊 [[03 - Spring Boot/00 - Concept Map/Phase 11 - Production - Observability & Operations|Phase 11 — Production: Observability & Operations]] · `0/13`
- ⚡ [[03 - Spring Boot/00 - Concept Map/Phase 12 - Async, Scheduling, Caching, Resilience|Phase 12 — Async, Scheduling, Caching, Resilience]] · `0/10`
- 🌱 [[03 - Spring Boot/00 - Concept Map/Phase 13 - Messaging, Batch, Integration|Phase 13 — Messaging, Batch, Integration]] · `0/10`
- 🌀 [[03 - Spring Boot/00 - Concept Map/Phase 14 - Reactive Spring|Phase 14 — Reactive Spring (only after MVC is solid)]] · `0/10`
- 🌱 [[03 - Spring Boot/00 - Concept Map/Phase 15 - Architecture, Microservices, Spring Cloud|Phase 15 — Architecture, Microservices, Spring Cloud]] · `0/15`
- 🔬 [[03 - Spring Boot/00 - Concept Map/Phase 16 - Internals & Mastery|Phase 16 — Internals & Mastery]] · `0/11`

---

## Suggested build order (learn by shipping, not by reading)

1. Hello-world API with `@RestController` → covers 11–33, 81–103.
2. Add Postgres + JPA + Flyway + a real CRUD resource → covers 129–164.
3. Add validation + global error handling + DTOs → 106–110.
4. Add tests (slices + Testcontainers) → 165–180.
5. Add security (JWT) → 181–201.
6. Add Actuator, metrics, logging, Docker → 202–214.
7. Add caching, async, scheduling, retry → 215–224.
8. Only then: messaging, reactive, microservices.

---

- 🗃️ [[03 - Spring Boot/00 - Concept Map/01 - Version & Platform Reality|A. Version & Platform Reality (learn this first, it saves you from wrong tutorials)]] · `0/8`
- ⚙️ [[03 - Spring Boot/00 - Concept Map/02 - Container & Configuration - what the phases above missed|B. Container & Configuration — what the phases above missed]] · `0/8`
- 🌐 [[03 - Spring Boot/00 - Concept Map/03 - Web Layer - what the phases above missed|C. Web Layer — what the phases above missed]] · `0/16`
- 🗃️ [[03 - Spring Boot/00 - Concept Map/04 - JPA & Hibernate - the biggest real gap in the phases above|D. JPA & Hibernate — the biggest real gap in the phases above]] · `0/20`
- 🌱 [[03 - Spring Boot/00 - Concept Map/05 - Security - what the phases above missed|E. Security — what the phases above missed]] · `0/8`
- 🧪 [[03 - Spring Boot/00 - Concept Map/06 - Testing & Quality - what the phases above missed|F. Testing & Quality — what the phases above missed]] · `0/8`
- 🌱 [[03 - Spring Boot/00 - Concept Map/07 - Ecosystem Modules Not Yet Listed|G. Ecosystem Modules Not Yet Listed]] · `0/10`
- 🌱 [[03 - Spring Boot/00 - Concept Map/08 - Tooling & Daily Workflow|H. Tooling & Daily Workflow]] · `0/8`
- 🧪 [[03 - Spring Boot/00 - Concept Map/09 - The Trap List - bugs that compile, pass tests, and break in production|I. The Trap List — bugs that compile, pass tests, and break in production]] · `0/24`
- 🌱 [[03 - Spring Boot/00 - Concept Map/10 - Beliefs to unlearn|J. Beliefs to unlearn]] · `0/8`

---

## K. The 20 concepts an interviewer will actually ask about

IoC/DI · bean scopes · bean lifecycle · `@Autowired` resolution and `@Qualifier`/`@Primary` · circular dependencies · `@SpringBootApplication` breakdown · auto-configuration and `@ConditionalOn*` · starters · AOP terms and proxy types · self-invocation · `DispatcherServlet` request flow · `@Controller` vs `@RestController` · exception handling with `@ControllerAdvice` · `@Transactional` propagation and rollback rules · JPA entity states and dirty checking · N+1 and lazy loading · Spring Data derived queries · security filter chain · JWT vs session · test slices vs `@SpringBootTest`.

[Likely] If you can explain those twenty out loud with an example each, you can pass most Spring interviews — regardless of how many boxes are ticked in this file.

---

- 🌱 [[03 - Spring Boot/00 - Concept Map/11 - Appendix - everything I deliberately left out|L. Appendix — everything I deliberately left out (and why)]] · `0/17`

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("03 - Spring Boot/00 - Concept Map")'
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
