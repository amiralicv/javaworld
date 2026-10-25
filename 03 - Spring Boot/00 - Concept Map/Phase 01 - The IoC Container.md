---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 23
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🫘 Phase 1 — The IoC Container (the true core of Spring)

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/Phase 00 - Prerequisites|Phase 0 — Prerequisites (Spring will feel like magic without these)]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/Phase 02 - Bean Lifecycle, Scope, Extension Points|Phase 2 — Bean Lifecycle, Scope, Extension Points]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **11. IoC (Inversion of Control)** 🔴 — you stop calling `new`; the framework creates and connects objects for you. Control is inverted from your code to the container.
- [ ] **12. DI (Dependency Injection)** 🔴 — the concrete technique that implements IoC: dependencies are handed to an object from outside.
- [ ] **13. Why IoC exists** 🔴 — loose coupling, easier testing, replaceable implementations, central configuration.
- [ ] **14. Bean** 🔴 — any object created and managed by the Spring container.
- [ ] **15. IoC container** 🔴 — the thing that reads config, builds beans, wires them, manages their life.
- [ ] **16. `BeanFactory` vs `ApplicationContext`** 🔴 — BeanFactory = minimal container; ApplicationContext = BeanFactory + events, i18n, resource loading, auto post-processing.
- [ ] **17. `BeanDefinition`** 🟡 — the recipe of a bean (class, scope, dependencies) before the object exists. Spring reads definitions first, creates objects later.
- [ ] **18. Configuration metadata: annotations vs Java config vs XML** 🔴 — three ways to tell the container what beans exist. Modern default: annotations + Java config.
- [ ] **19. Component scanning (`@ComponentScan`)** 🔴 — Spring walks your packages and registers annotated classes as beans.
- [ ] **20. Stereotype annotations** 🔴 — `@Component`, `@Service`, `@Repository`, `@Controller`. Technically almost the same; they express intent (and `@Repository` adds exception translation).
- [ ] **21. `@Configuration` + `@Bean`** 🔴 — define beans by writing a factory method. Needed for third-party classes you cannot annotate.
- [ ] **22. Full vs lite `@Configuration` (`proxyBeanMethods`)** 🟡 — with full mode, calling one `@Bean` method from another returns the _same_ singleton, not a new object.
- [ ] **23. `@Autowired`** 🔴 — "give me a bean of this type".
- [ ] **24. Constructor vs setter vs field injection** 🔴 — constructor is the recommended one: immutable, no hidden nulls, testable without Spring. Field injection is convenient and bad.
- [ ] **25. Injection resolution rules** 🔴 — by type first, then by name/qualifier when several candidates match.
- [ ] **26. `@Qualifier`** 🔴 — pick a specific bean when many of the same type exist.
- [ ] **27. `@Primary`** 🔴 — mark the default winner among candidates.
- [ ] **28. Injecting collections and maps of beans** 🟡 — `List<Validator>` gives you every implementation; a powerful plugin pattern.
- [ ] **29. `@Resource`, `@Inject`, JSR-330** 🟢 — alternative standard annotations and how they differ from `@Autowired`.
- [ ] **30. `Optional`, `ObjectProvider`, `@Autowired(required=false)`** 🟡 — handling a dependency that may not exist.
- [ ] **31. Circular dependencies** 🔴 — A needs B, B needs A. Why constructor injection makes this fail loudly, and why that failure is a design signal.
- [ ] **32. `@Lazy`** 🟡 — create the bean on first use instead of at startup.
- [ ] **33. `@DependsOn`** 🟢 — force creation order when there is a hidden dependency.

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
