---
type: hub
series: Java
tags: [java, moc]
---

# ☕ Java

> [!abstract] 🧭 Navigation
> 🏠 [[00 - Home|Home]]

> [!info] 📖 What lives here
> **Core** — one note per Java concept, written by you. **Interview** — 690 questions with answers, code and traps.

## 🧱 Core concepts

Create a note in `01 - Java/Core/` from the **📝 Topic Note** template for each concept you learn.

```base
filters:
  and:
    - 'file.inFolder("01 - Java/Core")'
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

## 🎯 Interview prep

- 🗂️ [[01 - Java/Interview/00 - Overview|Interview Hub — 690 questions]]
- [[01 - Java/Interview/01 - Basics|Part 1 — Basics]]
- [[01 - Java/Interview/02 - OOP|Part 2 — OOP]]
- [[01 - Java/Interview/03 - Collections|Part 3 — Collections]]
- [[01 - Java/Interview/04 - Exceptions & Generics|Part 4 — Exceptions & Generics]]
- [[01 - Java/Interview/05 - Concurrency|Part 5 — Concurrency]]
- [[01 - Java/Interview/06 - JVM|Part 6 — JVM]]
- [[01 - Java/Interview/07 - Java 8 & Modern Java|Part 7 — Java 8 & Modern Java]]
- [[01 - Java/Interview/08 - IO & Reflection|Part 8 — IO & Reflection]]
- [[01 - Java/Interview/09 - Patterns & Puzzles|Part 9 — Patterns & Puzzles]]
