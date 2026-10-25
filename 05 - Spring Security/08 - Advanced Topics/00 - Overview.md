---
type: stage
series: Spring Security
topics: 5
tags: [spring-security, roadmap]
---

# 🔐 Advanced Topics

> [!abstract] 🧭 Navigation
> ⬅️ [[05 - Spring Security/07 - Testing Security/00 - Overview|07 - Testing Security]] · 🏠 [[05 - Spring Security/00 - Overview|Spring Security]] · ➡️ [[05 - Spring Security/09 - Production Hardening/00 - Overview|09 - Production Hardening]]

> Stage 18: Advanced topics — ACL, multi-tenancy, LDAP, SAML, and building custom infrastructure. These are specialist tools. most projects need 2–3 of these subsections at most — read the intros to decide which apply to you before going deep.

---

## Stage 18 — Advanced topics

- 🔐 [[05 - Spring Security/08 - Advanced Topics/18.1 Spring Security ACL|18.1 Spring Security ACL (Access Control List)]] · `0/14`
- 🧭 [[05 - Spring Security/08 - Advanced Topics/18.2 Multi-tenancy|18.2 Multi-tenancy]] · `0/10`
- 🔐 [[05 - Spring Security/08 - Advanced Topics/18.3 LDAP and Active Directory|18.3 LDAP and Active Directory]] · `0/12`
- 🔐 [[05 - Spring Security/08 - Advanced Topics/18.4 SAML 2.0|18.4 SAML 2.0]] · `0/13`
- 🔐 [[05 - Spring Security/08 - Advanced Topics/18.5 Building fully custom security infrastructure|18.5 Building fully custom security infrastructure]] · `0/10`

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("05 - Spring Security/08 - Advanced Topics")'
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
