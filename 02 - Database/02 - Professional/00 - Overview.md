---
tags: [database, sql, postgres, roadmap, tier2]
status: not-started
type: stage
series: Database
topics: 9
---

	
# 🗄️ Database & SQL & Postgres — Tier 2: PROFESSIONAL

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/01 - Must Know/00 - Overview|01 - Must Know]] · 🏠 [[02 - Database/00 - Overview|Database]] · ➡️ [[02 - Database/03 - Legend/00 - Overview|03 - Legend]]

Items 111–235. This is the tier that changes your salary. [Likely] most working developers stop somewhere in the middle of it.

---

- 🔍 [[02 - Database/02 - Professional/01 - Advanced query writing|L. Advanced query writing]] · `0/20`
- 🗄️ [[02 - Database/02 - Professional/02 - Postgres-specific data features|M. Postgres-specific data features]] · `0/15`
- 🧮 [[02 - Database/02 - Professional/03 - Views, functions, triggers|N. Views, functions, triggers]] · `0/11`
- 📇 [[02 - Database/02 - Professional/04 - Indexing, deeper|O. Indexing, deeper]] · `0/12`
- ⚡ [[02 - Database/02 - Professional/05 - Performance & tuning|P. Performance & tuning]] · `0/22`
- 🛰️ [[02 - Database/02 - Professional/06 - Partitioning & large data|Q. Partitioning & large data]] · `0/7`
- 🚦 [[02 - Database/02 - Professional/07 - Operations you must understand as a developer|R. Operations you must understand as a developer]] · `0/12`
- 🧩 [[02 - Database/02 - Professional/08 - Schema change without downtime|S. Schema change without downtime]] · `0/9`
- 🧠 [[02 - Database/02 - Professional/09 - Beyond a single Postgres|T. Beyond a single Postgres]] · `0/17`

---

### Tier 2 exit test

1. Solve a top-N-per-group problem two ways (window function and `LATERAL`) and explain which plan is better.
2. Take a slow endpoint, find the query with `pg_stat_statements`, read its plan, and cut its time by 10x.
3. Add a `NOT NULL` column to a 50-million-row table with no downtime and explain each step's lock level.
4. Explain MVCC, bloat and autovacuum to a colleague in five minutes without notes.

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("02 - Database/02 - Professional")'
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
