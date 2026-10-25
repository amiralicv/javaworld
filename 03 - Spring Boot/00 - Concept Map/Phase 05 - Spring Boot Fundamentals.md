---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 16
created: 2026-09-28
tags: [spring-boot, topic]
---

# 📚 Phase 5 — Spring Boot Fundamentals

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/Phase 04 - AOP|Phase 4 — AOP (Aspect-Oriented Programming)]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/Phase 06 - Spring MVC & Building REST APIs|Phase 6 — Spring MVC & Building REST APIs]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **81. What Boot adds to Spring** 🔴 — opinionated defaults, auto-configuration, starters, embedded server, production tooling. Boot is _not_ a different framework.
- [ ] **82. `@SpringBootApplication`** 🔴 — it is three annotations in one: `@SpringBootConfiguration` + `@EnableAutoConfiguration` + `@ComponentScan`.
- [ ] **83. `SpringApplication.run()`** 🔴 — what actually happens at startup, step by step.
- [ ] **84. Auto-configuration** 🔴 — Boot guesses your setup from the classpath and existing beans, and configures beans conditionally. Backs off the moment you define your own.
- [ ] **85. `AutoConfiguration.imports`** 🟡 — the registry file listing all auto-config classes (older versions used `spring.factories`).
- [ ] **86. Excluding auto-configuration** 🟡 — when Boot's guess is wrong.
- [ ] **87. Starters** 🔴 — curated dependency bundles (`spring-boot-starter-web`, `-data-jpa`, `-security`...).
- [ ] **88. Dependency management / BOM** 🔴 — the parent POM pins compatible versions so you don't play version roulette.
- [ ] **89. Embedded server** 🔴 — Tomcat/Jetty/Undertow inside your jar; no external app server needed.
- [ ] **90. Executable fat jar & layered jars** 🟡 — how packaging works and why layering helps Docker caching.
- [ ] **91. `CommandLineRunner` / `ApplicationRunner`** 🟡 — run code once after startup.
- [ ] **92. The auto-configuration report** 🔴 — `--debug` shows which configs matched and which did not. Your best debugging tool.
- [ ] **93. Failure analyzers** 🟡 — why Boot's startup errors are readable.
- [ ] **94. DevTools** 🟡 — restart on change, live reload, dev-only property defaults.
- [ ] **95. Spring Initializr** 🟡 — project generation; know what each checkbox pulls in.
- [ ] **96. Writing your own auto-configuration / starter** 🟢 — the real test of whether you understood phases 1–5.

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
