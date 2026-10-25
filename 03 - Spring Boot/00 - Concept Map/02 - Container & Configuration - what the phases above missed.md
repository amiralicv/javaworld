---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 8
created: 2026-09-28
tags: [spring-boot, topic]
---

# ⚙️ B. Container & Configuration — what the phases above missed

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/01 - Version & Platform Reality|A. Version & Platform Reality (learn this first, it saves you from wrong tutorials)]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/03 - Web Layer - what the phases above missed|C. Web Layer — what the phases above missed]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **279. Bean naming rules and `BeanNameGenerator`** 🟡 — the default bean name is the decapitalized class name; matters for `@Qualifier` and for overriding.
- [ ] **280. Bean overriding (and why Boot disables it by default)** 🟡 — two beans with the same name used to silently replace each other. Now it fails at startup, on purpose.
- [ ] **281. `@Order`, `Ordered`, `@Priority`** 🟡 — controls the order of filters, aspects, interceptors, and injected lists.
- [ ] **282. `@ConfigurationPropertiesScan`** 🟡 — register config classes without `@EnableConfigurationProperties`.
- [ ] **283. Configuration metadata & IDE autocomplete** 🟡 — the annotation processor that makes your own properties autocomplete in `application.yml`.
- [ ] **284. `ApplicationArguments` and command-line parsing** 🟡.
- [ ] **285. Null-safety annotations (`@Nullable`, `@NonNullApi`)** 🟢 — Spring's own contracts, useful with Kotlin.
- [ ] **286. Internationalization (`MessageSource`, `LocaleResolver`)** 🟡 — translated messages, including validation messages.

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
