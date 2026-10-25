---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 8
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🌱 H. Tooling & Daily Workflow

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/07 - Ecosystem Modules Not Yet Listed|G. Ecosystem Modules Not Yet Listed]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/09 - The Trap List - bugs that compile, pass tests, and break in production|I. The Trap List — bugs that compile, pass tests, and break in production]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **349. IDE support** 🟡 — bean navigation, autocomplete in yaml, live templates. Uses the metadata from item 283.
- [ ] **350. The `startup` actuator endpoint** 🟡 — shows what took long during startup.
- [ ] **351. Reading a Spring stack trace** 🔴 — find the _last_ line that belongs to your code; ignore the 60 framework frames above it.
- [ ] **352. Common startup failures and what they mean** 🔴 — port in use, no qualifying bean, circular reference, missing datasource, bean creation exception chains.
- [ ] **353. Remote debugging & conditional breakpoints** 🟡.
- [ ] **354. Profiling** 🟡 — async-profiler, JFR, heap dumps. Guessing at performance wastes weeks.
- [ ] **355. Structured logging + correlation IDs** 🔴 — without them, debugging across services is impossible.
- [ ] **356. CI pipeline for a Boot app** 🟡 — build, test, image, scan, deploy.

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
