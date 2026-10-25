---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 8
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🧪 F. Testing & Quality — what the phases above missed

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/05 - Security - what the phases above missed|E. Security — what the phases above missed]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/07 - Ecosystem Modules Not Yet Listed|G. Ecosystem Modules Not Yet Listed]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **331. `@ServiceConnection` with Testcontainers** 🔴 — Boot wires the container's URL into your test context automatically. Removes most Testcontainers boilerplate.
- [ ] **332. Docker Compose support at dev time** 🟡 — Boot starts your `compose.yaml` when you run the app locally.
- [ ] **333. `@Sql` and `@SqlGroup`** 🟡 — run SQL before/after a test.
- [ ] **334. Transactional tests and rollback** 🟡 — convenient, but they hide commit-time failures.
- [ ] **335. Coverage (JaCoCo) and what it does not prove** 🟡 — 90% coverage with no assertions is 0% testing.
- [ ] **336. Mutation testing (PIT)** 🟢 — measures whether your tests would actually catch a bug.
- [ ] **337. ArchUnit** 🟢 — enforce architecture rules as tests ("controllers must not touch repositories").
- [ ] **338. Load testing basics** 🟡 — k6 or Gatling; you cannot tune pools and timeouts without numbers.

## 📝 My Notes

> [!note] ✍️ In your own words
> What is it? Why does it exist? When should you **not** use it?

## 💻 Code

```java
// minimal working example
```

## ⚠️ Gotchas & Traps

-

## ❓ Self-Test

- [ ] I can explain this out loud in 2 minutes without notes
- [ ] I wrote working code for it without copying

## 🔗 Related

-
