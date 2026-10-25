---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 8
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🌱 E. Security — what the phases above missed

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/04 - JPA & Hibernate - the biggest real gap in the phases above|D. JPA & Hibernate — the biggest real gap in the phases above]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/06 - Testing & Quality - what the phases above missed|F. Testing & Quality — what the phases above missed]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **323. `AuthorizationManager`** 🟡 — the modern authorization abstraction replacing the old voter/decision manager model.
- [ ] **324. Where to put the current user** 🟡 — `SecurityContextHolder` strategies, and why it breaks with `@Async` and virtual threads unless you propagate it.
- [ ] **325. Remember-me and session fixation** 🟡.
- [ ] **326. API keys and machine-to-machine auth** 🟡 — client credentials grant, or a custom filter.
- [ ] **327. Domain object security (ACL)** 🟢 — "can this user edit _this specific_ row".
- [ ] **328. SAML / enterprise SSO** 🟢.
- [ ] **329. Secrets rotation and key management** 🟡 — signing keys, JWKS endpoints.
- [ ] **330. Audit logging** 🟡 — who did what, when; separate from application logs.

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
