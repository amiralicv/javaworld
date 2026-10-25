---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 17
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🌱 L. Appendix — everything I deliberately left out (and why)

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/10 - Beliefs to unlearn|J. Beliefs to unlearn]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

These are real, but they are edge modules. Do not open any of them until a project forces you to. Listed for completeness so you stop wondering what is missing.

- [ ] **389. Spring Data JDBC** 🟡 — the one genuine omission. A simpler alternative to JPA: no persistence context, no lazy loading, no dirty checking. Aggregate-based. Worth knowing that it exists as the "JPA is too much magic" option.
- [ ] **390. Spring Retry** 🟢 — `@Retryable`, `@Recover`. Older and simpler than Resilience4j.
- [ ] **391. Spring Cloud Stream** 🟢 — a binder abstraction so your code does not know if it is Kafka or Rabbit.
- [ ] **392. Spring Cloud Function** 🟢 — write a `Function<T,R>` and deploy it as an HTTP endpoint or a serverless function.
- [ ] **393. Spring Cloud Task** 🟢 — short-lived jobs.
- [ ] **394. Spring Cloud Kubernetes** 🟢 — config maps as property sources, discovery via the K8s API.
- [ ] **395. Spring Web Services** 🟢 — SOAP. Only if you touch enterprise or government systems.
- [ ] **396. Spring Statemachine** 🟢 — formal state machines as beans.
- [ ] **397. JMX support** 🟢 — exposing beans as managed MBeans. Mostly replaced by Actuator.
- [ ] **398. JNDI lookup** 🟢 — legacy app-server integration.
- [ ] **399. Spring Boot Loader internals** 🟢 — how a nested jar actually boots.
- [ ] **400. CDS / AppCDS** 🟢 — class data sharing to cut startup time without going native.
- [ ] **401. Project CRaC (checkpoint & restore)** 🟢 — snapshot a warmed-up JVM and restore it in milliseconds.
- [ ] **402. Spring's `TaskScheduler` / `TaskDecorator`** 🟢 — lower-level scheduling and context propagation onto worker threads.
- [ ] **403. `@ConfigurationPropertiesBinding` and custom converters for config** 🟢.
- [ ] **404. `@ServletComponentScan`** 🟢 — registering plain servlet-API filters and servlets.
- [ ] **405. Groovy / Spring Boot CLI** 🟢 — rarely used today.

**This list is now closed.** Anything beyond item 405 is a specific library's documentation, not a Spring concept.

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
