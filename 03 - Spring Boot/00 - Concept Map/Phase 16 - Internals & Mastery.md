---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 11
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🔬 Phase 16 — Internals & Mastery

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/Phase 15 - Architecture, Microservices, Spring Cloud|Phase 15 — Architecture, Microservices, Spring Cloud]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/01 - Version & Platform Reality|A. Version & Platform Reality (learn this first, it saves you from wrong tutorials)]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **260. Full startup sequence, source-level** 🟢 — from `run()` to `ApplicationReadyEvent`.
- [ ] **261. `SpringFactoriesLoader` & extension registration** 🟢.
- [ ] **262. `ApplicationContextInitializer` & `EnvironmentPostProcessor`** 🟢 — hooking in before the context exists.
- [ ] **263. Meta-annotations & composed annotations** 🟡 — building your own `@MyTransactionalService`.
- [ ] **264. Merged annotation model** 🟢 — how Spring resolves annotation attributes through layers.
- [ ] **265. Custom `Condition` implementations** 🟢.
- [ ] **266. Custom scopes** 🟢.
- [ ] **267. `ConversionService`, `Converter`, `Formatter`** 🟡 — how a String becomes a `LocalDate` in a request parameter.
- [ ] **268. Proxy internals & performance cost** 🟢.
- [ ] **269. Reading the Spring source & reference docs** 🔴 — the real final skill. The reference documentation is genuinely good; use it instead of tutorials.
- [ ] **270. Spring AI / newer modules** 🟢 — optional, follows the same container patterns you already know.

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
