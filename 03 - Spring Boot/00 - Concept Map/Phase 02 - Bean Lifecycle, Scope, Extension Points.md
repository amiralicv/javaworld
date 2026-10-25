---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 19
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🫘 Phase 2 — Bean Lifecycle, Scope, Extension Points

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/Phase 01 - The IoC Container|Phase 1 — The IoC Container (the true core of Spring)]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/Phase 03 - Configuration & Environment|Phase 3 — Configuration & Environment]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **34. Bean lifecycle overview** 🔴 — instantiate → populate dependencies → aware callbacks → post-process before init → init → post-process after init → in use → destroy.
- [ ] **35. `@PostConstruct` / `@PreDestroy`** 🔴 — run code after wiring, and before shutdown.
- [ ] **36. `InitializingBean` / `DisposableBean`** 🟡 — the interface-based version (couples you to Spring, so prefer the annotations).
- [ ] **37. `@Bean(initMethod, destroyMethod)`** 🟡 — lifecycle hooks for classes you don't own.
- [ ] **38. `*Aware` interfaces** 🟡 — `ApplicationContextAware`, `BeanNameAware`, `EnvironmentAware`: ask the container about itself.
- [ ] **39. `BeanPostProcessor`** 🟡 — intercept _every_ bean after creation. This is how AOP, `@Autowired`, `@Async` etc. are actually implemented.
- [ ] **40. `BeanFactoryPostProcessor`** 🟡 — change bean _definitions_ before any object is created.
- [ ] **41. `BeanDefinitionRegistryPostProcessor`** 🟢 — register brand-new bean definitions programmatically.
- [ ] **42. Scope: singleton** 🔴 — one instance per container (the default). Not the Singleton pattern; it is per-container.
- [ ] **43. Scope: prototype** 🔴 — new instance on every request; Spring does not manage its destruction.
- [ ] **44. Web scopes** 🟡 — `request`, `session`, `application`, `websocket`.
- [ ] **45. Scoped proxies** 🟡 — how a short-lived bean can be injected into a singleton without breaking.
- [ ] **46. Singleton + mutable state = bug** 🔴 — the single most common beginner mistake. Beans must be stateless or thread-safe.
- [ ] **47. `FactoryBean<T>`** 🟢 — a bean whose job is producing another bean; used heavily inside Spring itself.
- [ ] **48. `ApplicationContext` refresh sequence** 🟡 — the ordered startup steps of the container. Read it once; it explains a lot of "why does X happen before Y".
- [ ] **49. Application events (`ApplicationEvent`, `@EventListener`)** 🟡 — in-process publish/subscribe for decoupling components.
- [ ] **50. Built-in events** 🟡 — `ApplicationReadyEvent`, `ContextRefreshedEvent`, `ContextClosedEvent`.
- [ ] **51. Async events & `@TransactionalEventListener`** 🟢 — fire after commit, or on another thread.
- [ ] **52. `Lifecycle` / `SmartLifecycle`** 🟢 — start/stop components in a controlled order.

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
