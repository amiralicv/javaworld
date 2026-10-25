---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 10
created: 2026-09-28
tags: [spring-boot, topic]
---

# ⚡ Phase 12 — Async, Scheduling, Caching, Resilience

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/Phase 11 - Production - Observability & Operations|Phase 11 — Production: Observability & Operations]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/Phase 13 - Messaging, Batch, Integration|Phase 13 — Messaging, Batch, Integration]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **215. `@Async` and `TaskExecutor`** 🔴 — run a method on another thread; needs `@EnableAsync` and a properly sized pool.
- [ ] **216. `CompletableFuture` in Spring** 🟡 — returning async results.
- [ ] **217. Thread pool sizing & exhaustion** 🟡 — the default pool is rarely what you want.
- [ ] **218. `@Scheduled`** 🔴 — fixed rate, fixed delay, cron expressions.
- [ ] **219. Scheduling in multiple instances** 🟡 — the job runs N times unless you add locking (ShedLock, DB lock, leader election).
- [ ] **220. Cache abstraction** 🔴 — `@EnableCaching`, `@Cacheable`, `@CachePut`, `@CacheEvict`, keys, conditions.
- [ ] **221. Cache providers** 🟡 — simple map, Caffeine, Redis; local vs distributed and the invalidation problem.
- [ ] **222. Resilience4j** 🟡 — retry, circuit breaker, rate limiter, bulkhead, time limiter.
- [ ] **223. Retry & idempotency** 🔴 — retrying a non-idempotent operation creates duplicates.
- [ ] **224. Timeouts everywhere** 🔴 — no timeout means one slow dependency takes your whole app down.

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
