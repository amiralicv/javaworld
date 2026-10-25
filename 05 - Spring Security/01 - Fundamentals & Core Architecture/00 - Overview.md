---
type: stage
series: Spring Security
topics: 6
tags: [spring-security, roadmap]
---

# 🔐 Fundamentals & Core Architecture

> [!abstract] 🧭 Navigation
> 🏠 [[05 - Spring Security/00 - Overview|Spring Security]] · ➡️ [[05 - Spring Security/02 - Authentication, Passwords & Authorization/00 - Overview|02 - Authentication, Passwords & Authorization]]

> **How to use:** Tick `- [ ]` when you can _explain the concept out loud_ and _write code using it without copying_.

---

- 📚 [[05 - Spring Security/01 - Fundamentals & Core Architecture/Stage 0 - Prerequisites|Stage 0 — Prerequisites (do not skip)]] · `0/12`
- 📚 [[05 - Spring Security/01 - Fundamentals & Core Architecture/Stage 1 - Security fundamentals|Stage 1 — Security fundamentals (no framework, pure theory)]] · `0/25`
- 🔏 [[05 - Spring Security/01 - Fundamentals & Core Architecture/Stage 2 - Cryptography for developers|Stage 2 — Cryptography for developers (only what you need)]] · `0/22`
- 🛡️ [[05 - Spring Security/01 - Fundamentals & Core Architecture/Stage 3 - Web security threats|Stage 3 — Web security threats (know the enemy first)]] · `0/33`
- 🌐 [[05 - Spring Security/01 - Fundamentals & Core Architecture/Stage 4 - The Servlet layer|Stage 4 — The Servlet layer (the ground Spring Security stands on)]] · `0/13`
- 🔐 [[05 - Spring Security/01 - Fundamentals & Core Architecture/Stage 5 - Spring Security core architecture|Stage 5 — Spring Security core architecture (the heart)]] · `0/48`

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("05 - Spring Security/01 - Fundamentals & Core Architecture")'
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
