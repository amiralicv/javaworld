---
title: Phase 1 - Backend Foundation
phase: 1
window: Month 0-9
status: in-progress
tags:
  - roadmap
  - backend
type: stage
series: Java Data Engineering
topics: 9
---

# 🚀 Phase 1 — Backend Foundation (Month 0–9)

> [!abstract] 🧭 Navigation
> 🏠 [[06 - Java Data Engineering/00 - Overview|START HERE]] · ➡️ [[06 - Java Data Engineering/02 - Phase 2 - Data Foundations/00 - Overview|02 - Phase 2 - Data Foundations]]

> **Goal of this phase:** stop being someone who *writes Java* and become someone who *ships and operates a service.*
> Everything in Phase 2 and 3 assumes you already have this. Do not skip it because it is not exciting.

---

- ☕ [[06 - Java Data Engineering/01 - Phase 1 - Backend Foundation/1.1 Java, properly|1.1 Java, properly]] · `0/9`
- 🔬 [[06 - Java Data Engineering/01 - Phase 1 - Backend Foundation/1.2 Spring Boot - as an engineer, not a user|1.2 Spring Boot — as an engineer, not a user]] · `0/8`
- 🔍 [[06 - Java Data Engineering/01 - Phase 1 - Backend Foundation/1.3 SQL - the skill that decides everything later|1.3 SQL — the skill that decides everything later]] · `0/9`
- 🐧 [[06 - Java Data Engineering/01 - Phase 1 - Backend Foundation/1.4 Linux + the command line|1.4 Linux + the command line]] · `0/9`
- 🌿 [[06 - Java Data Engineering/01 - Phase 1 - Backend Foundation/1.5 Git - beyond commit and push|1.5 Git — beyond commit and push]] · `0/6`
- 🐳 [[06 - Java Data Engineering/01 - Phase 1 - Backend Foundation/1.6 Docker|1.6 Docker]] · `0/6`
- 🧪 [[06 - Java Data Engineering/01 - Phase 1 - Backend Foundation/1.7 Testing & code quality|1.7 Testing & code quality]] · `0/6`
- 📡 [[06 - Java Data Engineering/01 - Phase 1 - Backend Foundation/1.8 How the internet actually works|1.8 How the internet actually works]] · `0/6`
- 🏗️ [[06 - Java Data Engineering/01 - Phase 1 - Backend Foundation/01 - Phase 1 deliverables|Phase 1 deliverables]] · `0/4`

---

## Reading list for this phase

| Book | Why |
|---|---|
| *Effective Java* — Bloch | How to write Java that other engineers respect |
| *SQL Performance Explained* — Winand | Short, and permanently upgrades your database instinct |
| *The Pragmatic Programmer* | The professional habits nobody teaches you at work |
| *Designing Data-Intensive Applications* — Kleppmann (ch. 1–4) | Start it now. Slowly. It becomes the spine of Phase 3. |

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("06 - Java Data Engineering/01 - Phase 1 - Backend Foundation")'
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
