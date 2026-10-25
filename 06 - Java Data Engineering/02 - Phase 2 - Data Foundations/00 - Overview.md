---
title: Phase 2 - Data Foundations
phase: 2
window: Month 9-18
status: not-started
tags:
  - roadmap
  - data
type: stage
series: Java Data Engineering
topics: 7
---

# 🚀 Phase 2 — Data Foundations (Month 9–18)

> [!abstract] 🧭 Navigation
> ⬅️ [[06 - Java Data Engineering/01 - Phase 1 - Backend Foundation/00 - Overview|01 - Phase 1 - Backend Foundation]] · 🏠 [[06 - Java Data Engineering/00 - Overview|START HERE]] · ➡️ [[06 - Java Data Engineering/03 - Phase 3 - Pipelines and Distributed Systems/00 - Overview|03 - Phase 3 - Pipelines and Distributed Systems]]

> **Goal of this phase:** learn how data is *modeled, stored, and moved* — the thinking layer. Tools come in Phase 3. If you learn the tools before the thinking, you become a person who can run Airflow but cannot design a table.

---

- 🐍 [[06 - Java Data Engineering/02 - Phase 2 - Data Foundations/2.1 Python - your second language|2.1 Python — your second language]] · `0/10`
- 🚀 [[06 - Java Data Engineering/02 - Phase 2 - Data Foundations/2.2 Databases, deeply|2.2 Databases, deeply]] · `0/9`
- 🧩 [[06 - Java Data Engineering/02 - Phase 2 - Data Foundations/2.3 Data modeling - the real skill|2.3 Data modeling — the real skill]] · `0/10`
- 🔬 [[06 - Java Data Engineering/02 - Phase 2 - Data Foundations/2.4 Warehouses & analytical storage|2.4 Warehouses & analytical storage]] · `0/8`
- 🏭 [[06 - Java Data Engineering/02 - Phase 2 - Data Foundations/2.5 Ingestion patterns|2.5 Ingestion patterns]] · `0/7`
- 📈 [[06 - Java Data Engineering/02 - Phase 2 - Data Foundations/2.6 Statistics - the honest minimum|2.6 Statistics — the honest minimum]] · `0/6`
- 🏗️ [[06 - Java Data Engineering/02 - Phase 2 - Data Foundations/01 - Phase 2 deliverables|Phase 2 deliverables]] · `0/3`

---

## Job-market note

**At the end of Phase 2 you are already hireable as a junior data engineer.** You do not need Phase 3 to start applying — Phase 3 is what you learn *on the job* while you are being paid, which is always faster than learning it alone.

Applying early is not cheating. It is the plan.

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("06 - Java Data Engineering/02 - Phase 2 - Data Foundations")'
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
