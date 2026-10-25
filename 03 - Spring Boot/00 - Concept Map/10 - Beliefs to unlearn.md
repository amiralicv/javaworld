---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 8
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🌱 J. Beliefs to unlearn

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/09 - The Trap List - bugs that compile, pass tests, and break in production|I. The Trap List — bugs that compile, pass tests, and break in production]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/11 - Appendix - everything I deliberately left out|L. Appendix — everything I deliberately left out (and why)]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **381. "Spring Boot replaced Spring."** — No. Boot is configuration and packaging on top of the same Spring container. [Certain]
- [ ] **382. "`@Service`, `@Component` and `@Repository` do different things."** — Almost nothing differs technically; only `@Repository` adds exception translation. The rest is intent. [Certain]
- [ ] **383. "Singleton scope means the Singleton pattern."** — It means one instance _per container_, not per JVM. [Certain]
- [ ] **384. "Annotations are magic."** — They are metadata. A `BeanPostProcessor` or proxy does the actual work. Once you accept this, the framework stops being mysterious. [Certain]
- [ ] **385. "Reactive is faster."** — It gives higher concurrency per thread, not lower latency, and it costs you debuggability. With virtual threads, most apps do not need it. [Likely]
- [ ] **386. "Microservices are the professional choice."** — They trade code complexity for operational and distributed-systems complexity. Most teams under ~30 engineers are better off with a modular monolith. [Likely]
- [ ] **387. "Spring Data JPA means I do not need SQL."** — The opposite. It generates SQL you are responsible for. [Certain]
- [ ] **388. "If it works locally it works in production."** — Concurrency, data volume, network failure and time zones are the four things your laptop hides from you. [Certain]

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
