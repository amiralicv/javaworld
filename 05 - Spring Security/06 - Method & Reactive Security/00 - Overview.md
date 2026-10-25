---
type: stage
series: Spring Security
topics: 10
tags: [spring-security, roadmap]
---

# 🔐 Method & Reactive Security

> [!abstract] 🧭 Navigation
> ⬅️ [[05 - Spring Security/05 - OAuth2 & OpenID Connect/00 - Overview|05 - OAuth2 & OpenID Connect]] · 🏠 [[05 - Spring Security/00 - Overview|Spring Security]] · ➡️ [[05 - Spring Security/07 - Testing Security/00 - Overview|07 - Testing Security]]

> Stages 15–16: Method security, and Reactive/WebFlux security.

---

## Stage 15 — Method-level security

- 🎯 [[05 - Spring Security/06 - Method & Reactive Security/15.1 Enabling method security|15.1 Enabling method security]] · `0/7`
- 🔐 [[05 - Spring Security/06 - Method & Reactive Security/15.2 The annotations|15.2 The annotations]] · `0/8`
- 🔬 [[05 - Spring Security/06 - Method & Reactive Security/15.3 AuthorizationManager-based method security|15.3 `AuthorizationManager`-based method security (Spring Security 6 internals)]] · `0/5`
- 🧮 [[05 - Spring Security/06 - Method & Reactive Security/15.4 Writing expressions|15.4 Writing expressions]] · `0/8`
- 🎯 [[05 - Spring Security/06 - Method & Reactive Security/15.5 Design patterns for method security|15.5 Design patterns for method security]] · `0/8`

---

## Stage 16 — Reactive security (Spring WebFlux)

- 🌀 [[05 - Spring Security/06 - Method & Reactive Security/16.1 Why reactive security is a different model|16.1 Why reactive security is a different model]] · `0/6`
- 🌀 [[05 - Spring Security/06 - Method & Reactive Security/16.2 Core reactive types|16.2 Core reactive types]] · `0/11`
- 🌀 [[05 - Spring Security/06 - Method & Reactive Security/16.3 Configuring reactive security|16.3 Configuring reactive security]] · `0/8`
- 🌀 [[05 - Spring Security/06 - Method & Reactive Security/16.4 Method security in reactive apps|16.4 Method security in reactive apps]] · `0/4`
- 🌀 [[05 - Spring Security/06 - Method & Reactive Security/16.5 Reactive gotchas|16.5 Reactive gotchas]] · `0/4`

---

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("05 - Spring Security/06 - Method & Reactive Security")'
    - 'note.type == "topic"'
formulas:
  state: 'if(note.status == "done", "✅ done", if(note.status == "learning", "🟨 learning", "⬜ todo"))'
views:
  - type: table
    name: 📊 Progress
    order:
      - file.name
      - formula.state
      - note.items
    sort:
      - property: file.name
        direction: ASC
```
