---
type: stage
series: Spring Security
topics: 14
tags: [spring-security, roadmap]
---

# 🔐 Authentication, Passwords & Authorization

> [!abstract] 🧭 Navigation
> ⬅️ [[05 - Spring Security/01 - Fundamentals & Core Architecture/00 - Overview|01 - Fundamentals & Core Architecture]] · 🏠 [[05 - Spring Security/00 - Overview|Spring Security]] · ➡️ [[05 - Spring Security/03 - Filter Chain, Sessions, CSRF & CORS/00 - Overview|03 - Filter Chain, Sessions, CSRF & CORS]]

> Stages 6–8: Authentication deep dive, Password management, Authorization. Prerequisite: finish Stage 5 (core architecture) first — everything here assumes you can draw the filter chain from memory.

---

## Stage 6 — Authentication deep dive

- 🔐 [[05 - Spring Security/02 - Authentication, Passwords & Authorization/6.1 The authentication flow|6.1 The authentication flow]] · `0/5`
- 🎟️ [[05 - Spring Security/02 - Authentication, Passwords & Authorization/6.2 Authentication token types|6.2 Authentication token types]] · `0/11`
- 🔐 [[05 - Spring Security/02 - Authentication, Passwords & Authorization/6.3 AuthenticationManager and providers|6.3 `AuthenticationManager` and providers]] · `0/8`
- 🔐 [[05 - Spring Security/02 - Authentication, Passwords & Authorization/6.4 Built-in AuthenticationProviders|6.4 Built-in `AuthenticationProvider`s]] · `0/11`
- 🔐 [[05 - Spring Security/02 - Authentication, Passwords & Authorization/6.5 UserDetails and UserDetailsService|6.5 `UserDetails` and `UserDetailsService`]] · `0/13`
- 🔐 [[05 - Spring Security/02 - Authentication, Passwords & Authorization/6.6 Reading the current user|6.6 Reading the current user]] · `0/12`
- 🔐 [[05 - Spring Security/02 - Authentication, Passwords & Authorization/6.7 Authentication events|6.7 Authentication events]] · `0/7`
- 🔑 [[05 - Spring Security/02 - Authentication, Passwords & Authorization/Stage 7 - Passwords and credential management|Stage 7 — Passwords and credential management]] · `0/30`

---

## Stage 8 — Authorization

- 🧩 [[05 - Spring Security/02 - Authentication, Passwords & Authorization/8.1 Core authorization model|8.1 Core authorization model]] · `0/7`
- 🔐 [[05 - Spring Security/02 - Authentication, Passwords & Authorization/8.2 Roles vs authorities|8.2 Roles vs authorities]] · `0/9`
- 🔐 [[05 - Spring Security/02 - Authentication, Passwords & Authorization/8.3 URL-level authorization|8.3 URL-level (request) authorization]] · `0/18`
- 🧮 [[05 - Spring Security/02 - Authentication, Passwords & Authorization/8.4 SpEL in security expressions|8.4 SpEL in security expressions]] · `0/9`
- 🔐 [[05 - Spring Security/02 - Authentication, Passwords & Authorization/8.5 Ownership and object-level authorization|8.5 Ownership and object-level authorization]] · `0/10`
- 🔐 [[05 - Spring Security/02 - Authentication, Passwords & Authorization/8.6 Failure handling|8.6 Failure handling]] · `0/10`

---

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("05 - Spring Security/02 - Authentication, Passwords & Authorization")'
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
