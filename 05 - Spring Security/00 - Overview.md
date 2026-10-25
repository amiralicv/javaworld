---
type: hub
series: Spring Security
tags: [spring-security, moc]
---

# 🔐 Spring Security

> [!abstract] 🧭 Navigation
> 🏠 [[00 - Home|Home]]

> [!info] 📖 What this track covers
> Security theory, crypto and web attacks first — then the filter chain, authentication, authorization, JWT, OAuth2, testing and production hardening.

## 🗺️ Stages

| # | Stage | Roadmap stages | Topics |
|---|---|---|---|
| 01 | 📚 [[05 - Spring Security/01 - Fundamentals & Core Architecture/00 - Overview\|Fundamentals & Core Architecture]] | 0–5 | 6 |
| 02 | 🔑 [[05 - Spring Security/02 - Authentication, Passwords & Authorization/00 - Overview\|Authentication, Passwords & Authorization]] | 6–8 | 14 |
| 03 | 🛡️ [[05 - Spring Security/03 - Filter Chain, Sessions, CSRF & CORS/00 - Overview\|Filter Chain, Sessions, CSRF & CORS]] | 9–11 | 13 |
| 04 | 🎟️ [[05 - Spring Security/04 - Login Mechanisms & JWT/00 - Overview\|Login Mechanisms & JWT]] | 12–13 | 17 |
| 05 | 🪪 [[05 - Spring Security/05 - OAuth2 & OpenID Connect/00 - Overview\|OAuth2 & OpenID Connect]] | 14 | 7 |
| 06 | 🌀 [[05 - Spring Security/06 - Method & Reactive Security/00 - Overview\|Method & Reactive Security]] | 15–16 | 10 |
| 07 | 🧪 [[05 - Spring Security/07 - Testing Security/00 - Overview\|Testing Security]] | 17 | 7 |
| 08 | 🧠 [[05 - Spring Security/08 - Advanced Topics/00 - Overview\|Advanced Topics]] | 18 | 5 |
| 09 | 🚦 [[05 - Spring Security/09 - Production Hardening/00 - Overview\|Production Hardening]] | 19 | 9 |
| 10 | 🏗️ [[05 - Spring Security/10 - Project Ladder/00 - Overview\|Project Ladder]] | 20 | 6 |

> [!tip] 🎯 How to work through it
> 1. Open a stage, then a topic note.
> 2. Learn → write **📝 My Notes** in your own words → write **💻 Code**.
> 3. Tick boxes only when you can explain them out loud. Update `status` as you go.

## 📊 Progress

```base
filters:
  and:
    - 'file.inFolder("05 - Spring Security")'
    - 'note.type == "topic"'
formulas:
  state: 'if(note.status == "done", "✅ done", if(note.status == "learning", "🟨 learning", "⬜ todo"))'
views:
  - type: table
    name: 📊 Progress
    groupBy:
      property: note.stage
      direction: ASC
    order:
      - file.name
      - formula.state
      - note.items
    sort:
      - property: file.name
        direction: ASC
```
