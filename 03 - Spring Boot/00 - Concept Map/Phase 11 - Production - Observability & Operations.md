---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 13
created: 2026-09-28
tags: [spring-boot, topic]
---

# 📊 Phase 11 — Production: Observability & Operations

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/Phase 10 - Spring Security|Phase 10 — Spring Security]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/Phase 12 - Async, Scheduling, Caching, Resilience|Phase 12 — Async, Scheduling, Caching, Resilience]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **202. Spring Boot Actuator** 🔴 — health, info, metrics, env, mappings, loggers endpoints.
- [ ] **203. Securing and exposing actuator endpoints** 🔴 — do not open `/actuator/env` to the world.
- [ ] **204. Health indicators, liveness & readiness** 🔴 — what Kubernetes actually probes.
- [ ] **205. Micrometer & metrics** 🟡 — counters, gauges, timers, `@Timed`.
- [ ] **206. Prometheus + Grafana** 🟡 — scraping and dashboards.
- [ ] **207. Distributed tracing** 🟡 — Micrometer Tracing / OpenTelemetry, trace and span IDs across services.
- [ ] **208. Logging** 🔴 — SLF4J + Logback, levels, patterns, MDC, correlation IDs, structured JSON logs.
- [ ] **209. Graceful shutdown** 🟡 — finish in-flight requests before dying.
- [ ] **210. Startup performance** 🟡 — lazy initialization, class data sharing, what actually costs time.
- [ ] **211. AOT processing & GraalVM native images** 🟢 — near-instant startup, at the cost of reflection restrictions.
- [ ] **212. Virtual threads (Loom)** 🟡 — high concurrency without going reactive.
- [ ] **213. Containerizing Spring Boot** 🔴 — Dockerfile, layered jars, buildpacks, JVM memory flags in containers.
- [ ] **214. Twelve-factor app principles** 🟡 — config, logs, stateless processes, disposability.

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
