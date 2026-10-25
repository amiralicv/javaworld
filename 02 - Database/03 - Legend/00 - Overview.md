---
tags: [database, sql, postgres, roadmap, tier3]
status: not-started
type: stage
series: Database
topics: 8
---

# 🗄️ Database & SQL & Postgres — Tier 3: LEGEND

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/02 - Professional/00 - Overview|02 - Professional]] · 🏠 [[02 - Database/00 - Overview|Database]]

Items 236–305. Internals, theory, and distributed systems.

**Honest warning:** [Likely] none of this makes you more useful at work next month. It makes you the person who can explain *why* Tier 2 behaves the way it does, and it is what you need to work on databases rather than merely with them. Do not start here to feel advanced.

---

- 🔬 [[02 - Database/03 - Legend/01 - Postgres storage internals|U. Postgres storage internals]] · `0/12`
- 💽 [[02 - Database/03 - Legend/02 - Durability, recovery, WAL|V. Durability, recovery, WAL]] · `0/8`
- ⚡ [[02 - Database/03 - Legend/03 - Query planner & optimizer internals|W. Query planner & optimizer internals]] · `0/12`
- 🔄 [[02 - Database/03 - Legend/04 - Concurrency control theory|X. Concurrency control theory]] · `0/8`
- 🛰️ [[02 - Database/03 - Legend/05 - Distributed data|Y. Distributed data]] · `0/11`
- 🔬 [[02 - Database/03 - Legend/06 - Storage engines & systems research|Z. Storage engines & systems research]] · `0/7`
- 🗄️ [[02 - Database/03 - Legend/07 - Extending Postgres|AA. Extending Postgres]] · `0/7`
- 🗄️ [[02 - Database/03 - Legend/08 - Practice that actually earns the title|AB. Practice that actually earns the title]] · `0/5`

---

### Honest priority note

If you are a backend developer, the highest-value items in this whole file are **238–241 (tuple headers and MVCC), 256–261 (how the planner estimates), and 271–272 (write skew and SSI)**. Those three clusters explain real production behaviour you will meet. The rest is craft and curiosity.

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("02 - Database/03 - Legend")'
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
