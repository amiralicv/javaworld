---
type: topic
series: Spring Boot
stage: "01 - IoC, DI & Container"
status: todo
items: 8
created: 2026-09-28
tags: [spring-boot, topic]
---

# 📚 Stage 0 — Prerequisites

> [!abstract] 🧭 Navigation
> 🔼 [[03 - Spring Boot/01 - IoC, DI & Container/00 - Overview|01 - IoC, DI & Container]] · ➡️ [[03 - Spring Boot/01 - IoC, DI & Container/1.1 The core idea|1.1 The core idea]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] 0.1 Java interfaces, abstract classes, and why "program to an interface" matters here specifically
- [ ] 0.2 Reflection basics — Spring is built on it, you should recognize `Class<?>`, `Method`, `Field`, `Annotation` usage
- [ ] 0.3 Dynamic proxies (`java.lang.reflect.Proxy`) and the concept of a proxy object — needed for AOP, transactions, and method security
- [ ] 0.4 Annotations — how they're defined, retention policy (`RUNTIME` vs `CLASS` vs `SOURCE`), and why Spring's are almost all `RUNTIME`
- [ ] 0.5 Generics, especially bounded wildcards — Spring's type resolution leans on this
- [ ] 0.6 Design patterns you'll meet by name constantly: Factory, Singleton, Proxy, Template Method, Observer, Strategy
- [ ] 0.7 Maven/Gradle basics — dependency scopes, BOM (Bill of Materials) imports
- [ ] 0.8 Classpath scanning concept — how a JVM app discovers classes at runtime

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
