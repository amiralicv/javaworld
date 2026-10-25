---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 17
created: 2026-09-28
tags: [spring-boot, topic]
---

# ⚙️ Phase 3 — Configuration & Environment

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/Phase 02 - Bean Lifecycle, Scope, Extension Points|Phase 2 — Bean Lifecycle, Scope, Extension Points]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/Phase 04 - AOP|Phase 4 — AOP (Aspect-Oriented Programming)]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **53. Externalized configuration** 🔴 — never hardcode values that change between environments.
- [ ] **54. `Environment` abstraction** 🔴 — the unified view over all sources of properties.
- [ ] **55. `PropertySource`** 🟡 — one source of properties (file, env vars, command line, system properties).
- [ ] **56. Property precedence order** 🔴 — command line > env vars > profile files > application file > defaults. Know this or you will lose hours.
- [ ] **57. `@Value`** 🔴 — inject a single property into a field or parameter.
- [ ] **58. SpEL (Spring Expression Language)** 🟡 — small expression language usable inside annotations: `#{...}`, `${...}`, operators, bean references.
- [ ] **59. `@ConfigurationProperties`** 🔴 — bind a whole group of properties into a typed object. Better than scattering `@Value` everywhere.
- [ ] **60. Relaxed binding** 🟡 — `my-prop`, `myProp`, `MY_PROP` all bind to the same field.
- [ ] **61. Validating configuration** 🟡 — `@Validated` on config classes so bad config fails at startup, not at 3am.
- [ ] **62. Profiles (`@Profile`, `spring.profiles.active`)** 🔴 — different beans and config per environment (dev, test, prod).
- [ ] **63. `application.properties` vs `application.yml`** 🔴 — same power, different syntax; yaml handles nesting and lists better.
- [ ] **64. Profile-specific files & config groups** 🟡 — `application-dev.yml`, `spring.config.import`, config trees.
- [ ] **65. `@Conditional` and `@ConditionalOnX`** 🔴 — create a bean only if some condition holds. This is the mechanism auto-configuration is built on.
- [ ] **66. `@Import`, `ImportSelector`, `ImportBeanDefinitionRegistrar`** 🟢 — pull configuration classes in programmatically; how `@EnableX` annotations work.
- [ ] **67. Resource abstraction (`Resource`, `ResourceLoader`)** 🟡 — read classpath files, filesystem files and URLs the same way.
- [ ] **68. XML configuration** 🟢 — legacy, but you will meet it in old codebases.
- [ ] **69. Secrets handling** 🟡 — env vars, vaults, config server; never in git.

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
