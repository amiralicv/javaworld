---
type: hub
series: Database
tags: [database, moc]
---

# 🗄️ Database — SQL & PostgreSQL

> [!abstract] 🧭 Navigation
> 🏠 [[00 - Home|Home]]

> [!info] 📖 What this track covers
> SQL and PostgreSQL in three tiers: what every backend developer must know, what a professional uses daily, and the internals that make you the database person on the team.

## 🧗 Tiers

| Level | Tier | Topics |
|---|---|---|
| 🟢 | [[02 - Database/01 - Must Know/00 - Overview\|Must Know]] | 11 |
| 🟡 | [[02 - Database/02 - Professional/00 - Overview\|Professional]] | 9 |
| 🔴 | [[02 - Database/03 - Legend/00 - Overview\|Legend]] | 8 |

## 🧰 Reference

- 🐘 [[02 - Database/04 - PostgreSQL Cheat Sheet|PostgreSQL Cheat Sheet]]
- 📄 [[02 - Database/Resources/SQL Execution Pipeline.pdf|SQL Execution Pipeline (PDF)]]

## 📊 Progress

```base
filters:
  and:
    - 'file.inFolder("02 - Database")'
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
