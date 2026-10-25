---
type: stage
series: Spring Security
topics: 13
tags: [spring-security, roadmap]
---

# 🔐 Filter Chain, Sessions, CSRF & CORS

> [!abstract] 🧭 Navigation
> ⬅️ [[05 - Spring Security/02 - Authentication, Passwords & Authorization/00 - Overview|02 - Authentication, Passwords & Authorization]] · 🏠 [[05 - Spring Security/00 - Overview|Spring Security]] · ➡️ [[05 - Spring Security/04 - Login Mechanisms & JWT/00 - Overview|04 - Login Mechanisms & JWT]]

> Stages 9–11: Configuration DSL, Session management, CSRF / CORS / Security headers. Prerequisite: Stages 6–8. From here on you should be writing code for every checkbox, not just reading.

---

## Stage 9 — Configuration: the DSL and how to shape the filter chain

- ⚙️ [[05 - Spring Security/03 - Filter Chain, Sessions, CSRF & CORS/9.1 Configuration basics|9.1 Configuration basics]] · `0/10`
- 🔐 [[05 - Spring Security/03 - Filter Chain, Sessions, CSRF & CORS/9.2 Multiple filter chains|9.2 Multiple filter chains]] · `0/8`
- 🌐 [[05 - Spring Security/03 - Filter Chain, Sessions, CSRF & CORS/9.3 The full HttpSecurity API surface|9.3 The full `HttpSecurity` API surface]] · `0/28`
- ⚙️ [[05 - Spring Security/03 - Filter Chain, Sessions, CSRF & CORS/9.4 Common configuration recipes|9.4 Common configuration recipes]] · `0/10`
- 🔐 [[05 - Spring Security/03 - Filter Chain, Sessions, CSRF & CORS/9.5 Custom filters|9.5 Custom filters]] · `0/16`

---

## Stage 10 — Session management

- 🍪 [[05 - Spring Security/03 - Filter Chain, Sessions, CSRF & CORS/10.1 Session fundamentals in Spring Security|10.1 Session fundamentals in Spring Security]] · `0/9`
- 🍪 [[05 - Spring Security/03 - Filter Chain, Sessions, CSRF & CORS/10.2 Session fixation and concurrency|10.2 Session fixation and concurrency]] · `0/13`
- 🍪 [[05 - Spring Security/03 - Filter Chain, Sessions, CSRF & CORS/10.3 Session storage and scaling|10.3 Session storage and scaling]] · `0/13`
- 📊 [[05 - Spring Security/03 - Filter Chain, Sessions, CSRF & CORS/10.4 Logout|10.4 Logout]] · `0/13`
- 🔐 [[05 - Spring Security/03 - Filter Chain, Sessions, CSRF & CORS/10.5 Remember-me|10.5 Remember-me]] · `0/8`

---

## Stage 11 — CSRF, CORS, and security headers

- 🛡️ [[05 - Spring Security/03 - Filter Chain, Sessions, CSRF & CORS/11.1 CSRF in Spring Security|11.1 CSRF in Spring Security]] · `0/18`
- 🛡️ [[05 - Spring Security/03 - Filter Chain, Sessions, CSRF & CORS/11.2 CORS in Spring Security|11.2 CORS in Spring Security]] · `0/12`
- 🛡️ [[05 - Spring Security/03 - Filter Chain, Sessions, CSRF & CORS/11.3 Security response headers|11.3 Security response headers]] · `0/21`

---

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("05 - Spring Security/03 - Filter Chain, Sessions, CSRF & CORS")'
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
