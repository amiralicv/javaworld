---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 11
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🪄 Phase 4 — AOP (Aspect-Oriented Programming)

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/Phase 03 - Configuration & Environment|Phase 3 — Configuration & Environment]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/Phase 05 - Spring Boot Fundamentals|Phase 5 — Spring Boot Fundamentals]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **70. Cross-cutting concern** 🔴 — logging, security, transactions, caching: logic that repeats everywhere and belongs to no single class.
- [ ] **71. AOP core idea** 🔴 — extract that repeated logic and weave it in around your methods automatically.
- [ ] **72. Vocabulary** 🔴 — aspect, join point, pointcut, advice, target, proxy, weaving. Learn these six words properly.
- [ ] **73. `@Aspect` + `@EnableAspectJAutoProxy`** 🟡 — declaring an aspect.
- [ ] **74. Advice types** 🟡 — `@Before`, `@After`, `@AfterReturning`, `@AfterThrowing`, `@Around`.
- [ ] **75. Pointcut expressions** 🟡 — `execution()`, `within()`, `@annotation()`, and combining them.
- [ ] **76. Proxies: JDK dynamic proxy vs CGLIB** 🔴 — interface-based vs subclass-based. Explains why `final` and `private` methods are not advised.
- [ ] **77. Self-invocation problem** 🔴 — calling `this.method()` skips the proxy, so `@Transactional`, `@Cacheable`, `@Async` silently do nothing. Extremely common bug.
- [ ] **78. Aspect ordering (`@Order`)** 🟡 — which aspect wraps which.
- [ ] **79. Spring AOP vs full AspectJ** 🟢 — proxy-based (method calls only) vs bytecode weaving (everything).
- [ ] **80. Where Spring itself uses AOP** 🔴 — transactions, security, caching, retry, async, validation. Understanding this de-mystifies half the framework.

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
