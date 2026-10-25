---
tags: [database, sql, postgres, roadmap, tier1]
status: in-progress
type: stage
series: Database
topics: 11
---

# 🗄️ Database & SQL & Postgres — Tier 1: MUST KNOW

> [!abstract] 🧭 Navigation
> 🏠 [[02 - Database/00 - Overview|Database]] · ➡️ [[02 - Database/02 - Professional/00 - Overview|02 - Professional]]

Items 1–110. Non-negotiable for any backend developer.
Rule for ticking a box: you can write it from memory *and* you know when it is the wrong choice.

---

- 🗄️ [[02 - Database/01 - Must Know/01 - What a database actually is|A. What a database actually is]] · `0/7`
- 🧱 [[02 - Database/01 - Must Know/02 - Data types & integrity|B. Data types & integrity]] · `0/14`
- 🔍 [[02 - Database/01 - Must Know/03 - Core SQL - reading data|C. Core SQL — reading data]] · `0/10`
- 🔗 [[02 - Database/01 - Must Know/04 - Joins|D. Joins]] · `0/9`
- 🔍 [[02 - Database/01 - Must Know/05 - Subqueries & set operations|E. Subqueries & set operations]] · `0/7`
- 🧮 [[02 - Database/01 - Must Know/06 - Expressions & functions|F. Expressions & functions]] · `0/8`
- 🗄️ [[02 - Database/01 - Must Know/07 - Writing data|G. Writing data]] · `0/7`
- 🔄 [[02 - Database/01 - Must Know/08 - Transactions & concurrency|H. Transactions & concurrency]] · `0/11`
- 📇 [[02 - Database/01 - Must Know/09 - Indexes - this belongs in tier 1, not later|I. Indexes — this belongs in tier 1, not later]] · `0/14`
- 🧩 [[02 - Database/01 - Must Know/10 - Data modelling|J. Data modelling]] · `0/13`
- 🗄️ [[02 - Database/01 - Must Know/11 - Postgres in practice|K. Postgres in practice]] · `0/10`

---

### Tier 1 exit test

You can call it done when you can, without help:
1. Model a small domain (users, orders, items) with correct keys and constraints.
2. Write a report query using joins, grouping and a `CASE`.
3. Explain why one of your queries is slow by reading `EXPLAIN ANALYZE`, and fix it with the right index.
4. Explain what happens when two transactions update the same row at the same time under Read Committed.

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("02 - Database/01 - Must Know")'
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
