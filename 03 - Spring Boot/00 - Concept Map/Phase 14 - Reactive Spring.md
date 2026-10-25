---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 10
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🌀 Phase 14 — Reactive Spring (only after MVC is solid)

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/Phase 13 - Messaging, Batch, Integration|Phase 13 — Messaging, Batch, Integration]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/Phase 15 - Architecture, Microservices, Spring Cloud|Phase 15 — Architecture, Microservices, Spring Cloud]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **235. Reactive programming concept** 🟡 — non-blocking, event-driven, backpressure.
- [ ] **236. Reactive Streams spec** 🟡 — Publisher, Subscriber, Subscription, Processor.
- [ ] **237. Project Reactor: `Mono` and `Flux`** 🟡 — 0..1 and 0..N async sequences.
- [ ] **238. Core operators** 🟡 — `map`, `flatMap`, `filter`, `zip`, `switchIfEmpty`, error operators.
- [ ] **239. Schedulers & threading** 🟡 — `subscribeOn`, `publishOn`, and why one blocking call ruins everything.
- [ ] **240. Spring WebFlux** 🟡 — annotated controllers on a non-blocking stack.
- [ ] **241. Functional endpoints** 🟢 — `RouterFunction`, `HandlerFunction`.
- [ ] **242. R2DBC** 🟢 — reactive database access; far less mature than JPA.
- [ ] **243. Reactive security & testing** 🟢.
- [ ] **244. When NOT to use reactive** 🔴 — with virtual threads available, most CRUD apps should stay blocking. Reactive costs debuggability.

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
