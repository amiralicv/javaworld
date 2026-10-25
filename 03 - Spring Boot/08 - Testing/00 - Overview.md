---
type: stage
series: Spring Boot
topics: 11
tags: [spring-boot, roadmap]
---

# 🌱 Testing

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/07 - Actuator & Production Readiness/00 - Overview|07 - Actuator & Production Readiness]] · 🏠 [[03 - Spring Boot/00 - Overview|Spring Boot]] · ➡️ [[03 - Spring Boot/09 - Project Ladder/00 - Overview|09 - Project Ladder]]

> Stage 10: Testing Spring & Spring Boot applications. You already met `@DataJpaTest` and `@WithMockUser`/`@SpringBootTest` in the other two roadmaps without their full context. This stage is that missing context — the general testing infrastructure they're both built on top of.

---

## Stage 10 — Testing Spring & Spring Boot applications

- 🧪 [[03 - Spring Boot/08 - Testing/10.1 The testing pyramid, applied to Spring apps specifically|10.1 The testing pyramid, applied to Spring apps specifically]] · `0/5`
- 🧪 [[03 - Spring Boot/08 - Testing/10.2 spring-boot-starter-test - what's actually bundled|10.2 `spring-boot-starter-test` — what's actually bundled]] · `0/5`
- 🧪 [[03 - Spring Boot/08 - Testing/10.3 @SpringBootTest in depth|10.3 `@SpringBootTest` in depth]] · `0/6`
- 🧪 [[03 - Spring Boot/08 - Testing/10.4 Slice test annotations tour|10.4 Slice test annotations tour]] · `0/7`
- 🌱 [[03 - Spring Boot/08 - Testing/10.5 Mocking dependencies inside the Spring context|10.5 Mocking dependencies inside the Spring context]] · `0/5`
- 🧪 [[03 - Spring Boot/08 - Testing/10.6 Testing web layer specifics|10.6 Testing web layer specifics]] · `0/5`
- 🧪 [[03 - Spring Boot/08 - Testing/10.7 Context caching - why test suite speed depends on this|10.7 Context caching — why test suite speed depends on this]] · `0/4`
- 🧪 [[03 - Spring Boot/08 - Testing/10.8 @ActiveProfiles and test-specific configuration|10.8 `@ActiveProfiles` and test-specific configuration]] · `0/4`
- 🧪 [[03 - Spring Boot/08 - Testing/10.9 Testing configuration and conditional logic itself|10.9 Testing configuration and conditional logic itself]] · `0/3`
- 🧪 [[03 - Spring Boot/08 - Testing/10.10 Testcontainers as general Spring Boot test infrastructure|10.10 Testcontainers as general Spring Boot test infrastructure (not just JPA)]] · `0/3`
- 🧪 [[03 - Spring Boot/08 - Testing/10.11 What to test at this layer generally|10.11 What to test at this layer generally]] · `0/5`

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("03 - Spring Boot/08 - Testing")'
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
