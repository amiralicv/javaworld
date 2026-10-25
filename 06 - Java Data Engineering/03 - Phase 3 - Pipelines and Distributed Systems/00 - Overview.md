---
title: Phase 3 - Pipelines and Distributed Systems
phase: 3
window: Month 18-30
status: not-started
tags:
  - roadmap
  - data-engineering
type: stage
series: Java Data Engineering
topics: 8
---

# 🚀 Phase 3 — Pipelines & Distributed Systems (Month 18–30)

> [!abstract] 🧭 Navigation
> ⬅️ [[06 - Java Data Engineering/02 - Phase 2 - Data Foundations/00 - Overview|02 - Phase 2 - Data Foundations]] · 🏠 [[06 - Java Data Engineering/00 - Overview|START HERE]] · ➡️ [[06 - Java Data Engineering/04 - Phase 4 - Production and Seniority/00 - Overview|04 - Phase 4 - Production and Seniority]]

> **Goal of this phase:** stop moving data by hand. Build systems that move it every day, at scale, without you watching — and that tell you when they break.
> This is where the "Data Engineer" title becomes true.

---

- 🔁 [[06 - Java Data Engineering/03 - Phase 3 - Pipelines and Distributed Systems/3.1 Orchestration - Airflow|3.1 Orchestration — Airflow]] · `0/9`
- 🔁 [[06 - Java Data Engineering/03 - Phase 3 - Pipelines and Distributed Systems/3.2 Transformation - dbt|3.2 Transformation — dbt]] · `0/8`
- 🌊 [[06 - Java Data Engineering/03 - Phase 3 - Pipelines and Distributed Systems/3.3 Streaming - Kafka|3.3 Streaming — Kafka]] · `0/10`
- 🛰️ [[06 - Java Data Engineering/03 - Phase 3 - Pipelines and Distributed Systems/3.4 Distributed processing - Spark|3.4 Distributed processing — Spark]] · `0/10`
- 🏭 [[06 - Java Data Engineering/03 - Phase 3 - Pipelines and Distributed Systems/3.5 Lakehouse table formats|3.5 Lakehouse table formats]] · `0/6`
- 🚀 [[06 - Java Data Engineering/03 - Phase 3 - Pipelines and Distributed Systems/3.6 Data quality & reliability|3.6 Data quality & reliability]] · `0/8`
- 🚀 [[06 - Java Data Engineering/03 - Phase 3 - Pipelines and Distributed Systems/3.7 Infrastructure as code|3.7 Infrastructure as code]] · `0/4`
- 🏗️ [[06 - Java Data Engineering/03 - Phase 3 - Pipelines and Distributed Systems/01 - Phase 3 deliverables|Phase 3 deliverables]] · `0/3`

---

## Where you stand at the end

You are a **mid-level data engineer**. In the local market you are in the top group. Internationally, you are the profile companies sponsor for relocation — because these systems are the same everywhere and nobody can fake them in an interview.

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("06 - Java Data Engineering/03 - Phase 3 - Pipelines and Distributed Systems")'
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
