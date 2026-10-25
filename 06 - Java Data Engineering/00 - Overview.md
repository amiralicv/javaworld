---
title: Java to Data Engineering - Roadmap
type: index
started: 
target_role: Data / Platform Engineer
location: Iran
tags:
  - roadmap
  - career
series: Java Data Engineering
---

# 🚀 Java → Data Engineering

> [!abstract] 🧭 Navigation
> 🏠 [[00 - Home|Home]]

> **The one rule:** a roadmap you do not review is decoration.
> Open this note **every Friday**. 10 minutes. Update the checkboxes. That habit is worth more than the content below.

---

## Why this path

You are not switching careers. You are **stacking** them.

```
Backend Engineer  →  Data Engineer  →  (optional) ML / Platform Engineer
   [you are here]      [the target]        [the option, not the plan]
```

Every step is a real job that pays. If you stop at step 2, you did not fail — you arrived. Nothing you learn in step 1 is thrown away in step 2. That is the whole point of choosing this route instead of restarting from zero as a data analyst.

**Three things make you paid, in this order:**
1. **Depth** — you are actually good, not "did a course"
2. **Scarcity** — few people can do what you do
3. **Closeness to money or risk** — you protect revenue or prevent loss

Technologies are just how you buy those three. Never fall in love with a tool.

---

## The map

| Phase | Note | Focus | Rough time |
|---|---|---|---|
| 1 | [[06 - Java Data Engineering/01 - Phase 1 - Backend Foundation/00 - Overview\|Phase 1 - Backend Foundation]] | Java, SQL, Linux, Git, Docker, testing | Month 0–9 |
| 2 | [[06 - Java Data Engineering/02 - Phase 2 - Data Foundations/00 - Overview\|Phase 2 - Data Foundations]] | Python, deep SQL, data modeling, warehouses | Month 9–18 |
| 3 | [[06 - Java Data Engineering/03 - Phase 3 - Pipelines and Distributed Systems/00 - Overview\|Phase 3 - Pipelines and Distributed Systems]] | Airflow, Kafka, Spark, dbt, file formats | Month 18–30 |
| 4 | [[06 - Java Data Engineering/04 - Phase 4 - Production and Seniority/00 - Overview\|Phase 4 - Production and Seniority]] | Kubernetes, observability, data quality, design | Month 30–48 |

Support notes:
- [[06 - Java Data Engineering/05 - Portfolio Projects|Portfolio Projects]] — what you actually build, with specs
- [[06 - Java Data Engineering/06 - Iran Playbook|Iran Playbook]] — sanctions reality, local stack, English, exit plan
- [[06 - Java Data Engineering/07 - Checkpoints and Traps|Checkpoints and Traps]] — how to know you are on track, and the ways people fail

---

## How to read the time estimates

The months assume **10–15 focused hours per week** on top of a job or study. Not 40. Not 2.

If you can only do 5 hours a week, double every number and **do not feel bad** — just do not lie to yourself about the date. A slow real plan beats a fast fake one.

**Time is not the measure. The exit criteria are.** Every topic below has a line called *"You are done when…"*. That sentence is the test, not the calendar.

---

## The weekly rhythm

| Day | What |
|---|---|
| Mon–Fri | Day job / study. Steal 30–60 min for the current topic. |
| Sat | 3–4 hour deep block on the current project. Real building, not videos. |
| One evening | Reading (book, docs, source code). No screen output required. |
| Friday 10 min | Open this vault. Tick boxes. Move one thing. Write one line in the log. |

**Ratio to protect: 70% building, 20% reading, 10% watching.**
If you flip that ratio you will feel productive and learn almost nothing. This is the single most common failure.

---

## Progress log

Add one line every Friday. Short is fine. Honest is required.

```
- 2026-08-28 — Started. Phase 1. SQL joins still shaky.
```

---

## Rules I am not allowed to break

- [ ] **No tutorial without a build.** Every course/book chapter ends with something I made.
- [ ] **Public work.** Every project lands in a public repo with a real README.
- [ ] **English every day.** 20 minutes minimum. Docs, not apps. See [[06 - Java Data Engineering/06 - Iran Playbook|Iran Playbook]].
- [ ] **One thing at a time.** No starting Kafka while SQL is still weak.
- [ ] **Deadline discipline.** If a phase runs 50% over its estimate, I review *why* — I do not just extend it.
- [ ] **Never chase a certificate I cannot register for.** Skill over badges.

---

## What "done" looks like at the end

You can be handed a sentence like *"we need yesterday's orders from three systems, cleaned, joined, tested, and in the warehouse by 6 AM every day, and someone must be paged when it breaks"* — and you can build that, run it, monitor it, and explain the trade-offs you chose.

That person gets hired anywhere. That is the whole target.

---

## 📊 Progress

```base
filters:
  and:
    - 'file.inFolder("06 - Java Data Engineering")'
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
