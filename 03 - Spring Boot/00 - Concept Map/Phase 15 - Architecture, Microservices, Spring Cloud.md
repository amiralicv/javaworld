---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 15
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🌱 Phase 15 — Architecture, Microservices, Spring Cloud

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/Phase 14 - Reactive Spring|Phase 14 — Reactive Spring (only after MVC is solid)]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/Phase 16 - Internals & Mastery|Phase 16 — Internals & Mastery]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **245. Layered architecture** 🔴 — controller → service → repository; what belongs in each layer.
- [ ] **246. Hexagonal / ports & adapters, clean architecture** 🟡 — keeping the framework out of your domain.
- [ ] **247. Package structure** 🟡 — by layer vs by feature (feature usually wins as the app grows).
- [ ] **248. Spring Modulith** 🟢 — enforcing module boundaries inside a monolith.
- [ ] **249. Monolith vs microservices** 🔴 — the honest trade-off; most teams should start monolithic.
- [ ] **250. Spring Cloud overview** 🟡 — what it is and which parts are still alive.
- [ ] **251. Config Server** 🟡 — centralized external configuration.
- [ ] **252. Service discovery** 🟡 — Eureka, Consul, or Kubernetes DNS.
- [ ] **253. API Gateway (Spring Cloud Gateway)** 🟡 — routing, filters, rate limiting.
- [ ] **254. Client-side load balancing** 🟡.
- [ ] **255. Distributed tracing across services** 🟡.
- [ ] **256. Saga pattern & distributed transactions** 🟢 — why 2PC is avoided and what replaces it.
- [ ] **257. Event-driven architecture** 🟢 — eventual consistency and its cost.
- [ ] **258. Contract testing** 🟢 — Spring Cloud Contract / Pact.
- [ ] **259. Spring Boot on Kubernetes** 🟡 — config maps, secrets, probes, scaling.

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
