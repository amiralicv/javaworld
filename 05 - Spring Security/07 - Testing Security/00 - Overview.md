---
type: stage
series: Spring Security
topics: 7
tags: [spring-security, roadmap]
---

# 🔐 Testing Security

> [!abstract] 🧭 Navigation
> ⬅️ [[05 - Spring Security/06 - Method & Reactive Security/00 - Overview|06 - Method & Reactive Security]] · 🏠 [[05 - Spring Security/00 - Overview|Spring Security]] · ➡️ [[05 - Spring Security/08 - Advanced Topics/00 - Overview|08 - Advanced Topics]]

> Stage 17: Testing security. A security rule you have not tested is a rule you don't actually have.

---

## Stage 17 — Testing security

- 🔐 [[05 - Spring Security/07 - Testing Security/17.1 Setup|17.1 Setup]] · `0/5`
- 🔐 [[05 - Spring Security/07 - Testing Security/17.2 Mocking authentication|17.2 Mocking authentication]] · `0/13`
- 🧪 [[05 - Spring Security/07 - Testing Security/17.3 What to actually test|17.3 What to actually test]] · `0/16`
- 🧪 [[05 - Spring Security/07 - Testing Security/17.4 Testing method security directly|17.4 Testing method security directly]] · `0/4`
- 🧪 [[05 - Spring Security/07 - Testing Security/17.5 Testing reactive security|17.5 Testing reactive security]] · `0/3`
- 🧪 [[05 - Spring Security/07 - Testing Security/17.6 Integration and end-to-end testing|17.6 Integration and end-to-end testing]] · `0/5`
- 🔐 [[05 - Spring Security/07 - Testing Security/17.7 Security-specific static analysis|17.7 Security-specific static analysis]] · `0/5`

---

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("05 - Spring Security/07 - Testing Security")'
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
