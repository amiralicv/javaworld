---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 8
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🗃️ A. Version & Platform Reality (learn this first, it saves you from wrong tutorials)

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/Phase 16 - Internals & Mastery|Phase 16 — Internals & Mastery]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/02 - Container & Configuration - what the phases above missed|B. Container & Configuration — what the phases above missed]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **271. Spring Framework vs Spring Boot vs Spring Cloud version lines** 🔴 — three different version numbers. Boot 3.x ships Framework 6.x. Tutorials that mix them will not compile.
- [ ] **272. The `javax` → `jakarta` namespace break** 🔴 — Boot 3 moved every `javax.persistence` / `javax.servlet` import to `jakarta.*`. This single change makes most pre-2023 tutorials wrong.
- [ ] **273. Java baseline per version** 🔴 — Boot 2 runs on Java 8+, Boot 3 needs Java 17+. Check before copying anything.
- [ ] **274. Removed / deprecated APIs you will still see in tutorials** 🔴 — `WebSecurityConfigurerAdapter`, `antMatchers`, `@MockBean`, `RestTemplate` as default choice. Know the replacements.
- [ ] **275. Release train & support windows** 🟡 — OSS support ends fast; commercial support extends it. Affects which version you start a project on.
- [ ] **276. How to read the migration guide** 🟡 — the wiki migration notes are the fastest way to upgrade a real project.
- [ ] **277. Spring's relation to Jakarta EE / CDI** 🟢 — Spring is not an EE server; it borrows the annotations, not the runtime.
- [ ] **278. The Spring reference documentation structure** 🔴 — core → web → data → boot. [Certain] It is better written than 95% of tutorials. Learn to navigate it.

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
