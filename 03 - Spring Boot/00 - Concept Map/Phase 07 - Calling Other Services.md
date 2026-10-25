---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 6
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🌐 Phase 7 — Calling Other Services (HTTP clients)

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/Phase 06 - Spring MVC & Building REST APIs|Phase 6 — Spring MVC & Building REST APIs]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/Phase 08 - Data Access & Transactions|Phase 8 — Data Access & Transactions]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **123. `RestTemplate`** 🟡 — the classic blocking client; maintenance mode but everywhere in existing code.
- [ ] **124. `RestClient`** 🔴 — the modern, fluent, blocking client. Default choice today.
- [ ] **125. `WebClient`** 🟡 — non-blocking/reactive client; also usable in blocking apps.
- [ ] **126. Declarative HTTP interfaces (`@HttpExchange`)** 🟡 — define a Java interface, Spring implements the calls.
- [ ] **127. Timeouts, connection pools, error decoding** 🔴 — the parts everyone forgets until production.
- [ ] **128. OpenFeign** 🟢 — declarative client from Spring Cloud.

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
