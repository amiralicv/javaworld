---
type: stage
series: Spring Security
topics: 17
tags: [spring-security, roadmap]
---

# 🔐 Login Mechanisms & JWT

> [!abstract] 🧭 Navigation
> ⬅️ [[05 - Spring Security/03 - Filter Chain, Sessions, CSRF & CORS/00 - Overview|03 - Filter Chain, Sessions, CSRF & CORS]] · 🏠 [[05 - Spring Security/00 - Overview|Spring Security]] · ➡️ [[05 - Spring Security/05 - OAuth2 & OpenID Connect/00 - Overview|05 - OAuth2 & OpenID Connect]]

> Stages 12–13: Login mechanisms in depth, JWT and stateless APIs. This is the part most real projects live in. Build something for every subsection, not just read.

---

## Stage 12 — Login mechanisms in depth

- 🌐 [[05 - Spring Security/04 - Login Mechanisms & JWT/12.1 HTTP Basic authentication|12.1 HTTP Basic authentication]] · `0/8`
- 🌐 [[05 - Spring Security/04 - Login Mechanisms & JWT/12.2 HTTP Digest authentication|12.2 HTTP Digest authentication]] · `0/4`
- 🗃️ [[05 - Spring Security/04 - Login Mechanisms & JWT/12.3 Form login|12.3 Form login]] · `0/17`
- 🔐 [[05 - Spring Security/04 - Login Mechanisms & JWT/12.4 Anonymous authentication|12.4 Anonymous authentication]] · `0/5`
- 🔐 [[05 - Spring Security/04 - Login Mechanisms & JWT/12.5 X.509 - certificate authentication|12.5 X.509 / certificate authentication]] · `0/6`
- 🔐 [[05 - Spring Security/04 - Login Mechanisms & JWT/12.6 Pre-authentication scenarios|12.6 Pre-authentication scenarios]] · `0/7`
- 🎟️ [[05 - Spring Security/04 - Login Mechanisms & JWT/12.7 One-time token - passwordless login|12.7 One-time token / passwordless login]] · `0/6`
- 🌐 [[05 - Spring Security/04 - Login Mechanisms & JWT/12.8 WebAuthn - Passkeys|12.8 WebAuthn / Passkeys]] · `0/6`
- 🔐 [[05 - Spring Security/04 - Login Mechanisms & JWT/12.9 Multi-factor authentication flows|12.9 Multi-factor authentication flows]] · `0/8`
- 🔐 [[05 - Spring Security/04 - Login Mechanisms & JWT/12.10 Choosing a mechanism|12.10 Choosing a mechanism]] · `0/5`

---

## Stage 13 — JWT and stateless APIs

- 🎟️ [[05 - Spring Security/04 - Login Mechanisms & JWT/13.1 Token theory|13.1 Token theory]] · `0/4`
- 🎟️ [[05 - Spring Security/04 - Login Mechanisms & JWT/13.2 JWT structure|13.2 JWT structure]] · `0/11`
- 🎟️ [[05 - Spring Security/04 - Login Mechanisms & JWT/13.3 JWT attacks|13.3 JWT attacks (learn these before writing any code)]] · `0/12`
- 🎟️ [[05 - Spring Security/04 - Login Mechanisms & JWT/13.4 Implementing JWT with Spring Security|13.4 Implementing JWT with Spring Security (the right way)]] · `0/18`
- 🎟️ [[05 - Spring Security/04 - Login Mechanisms & JWT/13.5 Implementing JWT manually|13.5 Implementing JWT manually (know it, then avoid it)]] · `0/9`
- 🎟️ [[05 - Spring Security/04 - Login Mechanisms & JWT/13.6 Refresh tokens and token lifecycle|13.6 Refresh tokens and token lifecycle]] · `0/12`
- 🌐 [[05 - Spring Security/04 - Login Mechanisms & JWT/13.7 Stateless API design concerns|13.7 Stateless API design concerns]] · `0/11`

---

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("05 - Spring Security/04 - Login Mechanisms & JWT")'
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
