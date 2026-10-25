---
type: stage
series: Spring Security
topics: 7
tags: [spring-security, roadmap]
---

# 🔐 OAuth2 & OpenID Connect

> [!abstract] 🧭 Navigation
> ⬅️ [[05 - Spring Security/04 - Login Mechanisms & JWT/00 - Overview|04 - Login Mechanisms & JWT]] · 🏠 [[05 - Spring Security/00 - Overview|Spring Security]] · ➡️ [[05 - Spring Security/06 - Method & Reactive Security/00 - Overview|06 - Method & Reactive Security]]

> Stage 14: OAuth2 and OpenID Connect — client, resource server, and authorization server. This is the densest single stage. Do not skip the theory subsections to jump to code — OAuth2 bugs are almost always conceptual, not syntax errors.

---

## Stage 14 — OAuth2 and OpenID Connect

- 🪪 [[05 - Spring Security/05 - OAuth2 & OpenID Connect/14.1 OAuth2 theory - roles and flows|14.1 OAuth2 theory — roles and flows]] · `0/20`
- 🪪 [[05 - Spring Security/05 - OAuth2 & OpenID Connect/14.2 OpenID Connect specifics|14.2 OpenID Connect specifics]] · `0/8`
- 🪪 [[05 - Spring Security/05 - OAuth2 & OpenID Connect/14.3 Spring Security as an OAuth2 Client|14.3 Spring Security as an OAuth2 Client (`oauth2Login`)]] · `0/25`
- 🪪 [[05 - Spring Security/05 - OAuth2 & OpenID Connect/14.4 Spring Security as an OAuth2 Resource Server|14.4 Spring Security as an OAuth2 Resource Server]] · `0/9`
- 🔐 [[05 - Spring Security/05 - OAuth2 & OpenID Connect/14.5 Spring Authorization Server|14.5 Spring Authorization Server (building your own)]] · `0/16`
- 🔐 [[05 - Spring Security/05 - OAuth2 & OpenID Connect/14.6 Third-party IdP integration patterns|14.6 Third-party IdP integration patterns]] · `0/4`
- 🪪 [[05 - Spring Security/05 - OAuth2 & OpenID Connect/14.7 OAuth2-OIDC pitfalls checklist|14.7 OAuth2/OIDC pitfalls checklist]] · `0/8`

---

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("05 - Spring Security/05 - OAuth2 & OpenID Connect")'
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
