---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 10
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🌱 Phase 13 — Messaging, Batch, Integration

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/Phase 12 - Async, Scheduling, Caching, Resilience|Phase 12 — Async, Scheduling, Caching, Resilience]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/Phase 14 - Reactive Spring|Phase 14 — Reactive Spring (only after MVC is solid)]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **225. Sync vs async communication** 🔴 — when a message beats an HTTP call.
- [ ] **226. Spring for Apache Kafka** 🟡 — producer, consumer, `@KafkaListener`, topics, partitions, consumer groups, offsets.
- [ ] **227. RabbitMQ / AMQP** 🟡 — exchanges, queues, bindings, `@RabbitListener`.
- [ ] **228. JMS** 🟢 — the older Java messaging standard.
- [ ] **229. Delivery guarantees** 🟡 — at-most-once, at-least-once, exactly-once (and why exactly-once is mostly a lie).
- [ ] **230. Dead letter queues & error handling** 🟡.
- [ ] **231. Transactional outbox pattern** 🟢 — how to publish an event and commit a DB change reliably.
- [ ] **232. Spring Batch** 🟢 — job, step, reader/processor/writer, chunk processing, restartability.
- [ ] **233. Spring Integration** 🟢 — enterprise integration patterns, channels, endpoints.
- [ ] **234. WebSocket & STOMP** 🟢 — real-time two-way communication.

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
