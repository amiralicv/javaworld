---
type: hub
series: Java Interview
tags: [java, interview, moc]
---

# ☕ Java Core Interview Reference — Master Index

> [!abstract] 🧭 Navigation
> 🏠 [[00 - Home|Home]] · ☕ [[01 - Java/00 - Overview|Java]]

> [!info] What this is
> A complete, 9-part Java core interview reference — **690 questions** with answers, code, tables, traps, and self-tests.
> Built for Obsidian: collapsible callouts, wiki links, tags, and checklists.
> Tags: #java #interview #core-java #moc

---

## 🗺️ The 9 Parts

| # | Part | Topics | Questions |
|---|------|--------|-----------|
| 1 | [[01 - Java/Interview/01 - Basics\|Part 1 — Basics]] | ☕ JVM/JDK/JRE, data types, operators, Strings, wrappers, `static`/`final`, constructors, arrays, access modifiers | Q1–Q70 |
| 2 | [[01 - Java/Interview/02 - OOP\|Part 2 — OOP]] | 🧬 Four pillars, inheritance, polymorphism, abstract vs interface, `equals`/`hashCode`, immutability, inner classes, enum/record/sealed | Q71–Q154 |
| 3 | [[01 - Java/Interview/03 - Collections\|Part 3 — Collections]] | 📦 Hierarchy, List family, **HashMap internals**, Maps, Sets, Queues, CME, Big-O cheat sheet | Q155–Q240 |
| 4 | [[01 - Java/Interview/04 - Exceptions & Generics\|Part 4 — Exceptions & Generics]] | ⚠️ Throwable hierarchy, try-with-resources, custom exceptions, type erasure, wildcards, **PECS** | Q241–Q316 |
| 5 | [[01 - Java/Interview/05 - Concurrency\|Part 5 — Concurrency]] | 🧵 Threads, `synchronized`, JMM, `volatile`, deadlock, thread pools, `CompletableFuture`, virtual threads | Q317–Q400 |
| 6 | [[01 - Java/Interview/06 - JVM\|Part 6 — JVM]] | 🧠 JVM architecture, heap generations, GC algorithms, class loading, memory leaks, tuning tools | Q401–Q468 |
| 7 | [[01 - Java/Interview/07 - Java 8 & Modern Java\|Part 7 — Java 8 & Modern Java]] | 🚀 Lambdas, functional interfaces, Streams, Collectors, `Optional`, `java.time`, Java 9–21 | Q469–Q556 |
| 8 | [[01 - Java/Interview/08 - IO & Reflection\|Part 8 — IO & Reflection]] | 💾 I/O and NIO, serialization, reflection, dynamic proxies, annotations | Q557–Q620 |
| 9 | [[01 - Java/Interview/09 - Patterns & Puzzles\|Part 9 — Patterns & Puzzles]] | 🎯 Design patterns, 28 output puzzles, coding round list, behavioural prep, final review sheet | Q621–Q690 |

---

## 📅 A 3-Week Study Plan

> [!tip] Do not read all nine parts in one week. Depth beats coverage.

**Week 1 — Foundations**
| Day | Task |
|---|---|
| 1–2 | Part 1 + write every code sample yourself |
| 3–4 | Part 2, focus on `equals`/`hashCode` and immutability |
| 5–7 | Part 3 — spend 2 full days on HashMap internals alone |

**Week 2 — Depth**
| Day | Task |
|---|---|
| 8–9 | Part 4 (PECS and erasure need slow reading) |
| 10–12 | Part 5 — the hardest part; do the concurrency coding exercises |
| 13–14 | Part 6 — GC and class loading |

**Week 3 — Modern Java + polish**
| Day | Task |
|---|---|
| 15–16 | Part 7 — write 20 stream one-liners from memory |
| 17 | Part 8 |
| 18 | Part 9 patterns |
| 19 | All 28 output puzzles, twice |
| 20 | Coding round list — 10 problems on paper |
| 21 | Final review sheet + prepare your 3 stories |

---

## 🎯 The Highest-Value Questions

If you only have one evening, learn these:

1. **HashMap internals** — Part 3, Q179–Q185
2. **equals/hashCode contract** — Part 2, Q118–Q123
3. **sleep vs wait, volatile vs synchronized** — Part 5, Q323, Q350
4. **ThreadPoolExecutor parameters** — Part 5, Q369
5. **Heap generations + memory leaks** — Part 6, Q413, Q421
6. **map vs flatMap + stream laziness** — Part 7, Q496, Q498
7. **Type erasure + PECS** — Part 4, Q299, Q308
8. **Immutable class design** — Part 2, Q128
9. **Composition over inheritance** — Part 2, Q75
10. **The 28 output puzzles** — Part 9

---

## 🧠 How to Actually Use This

> [!warning] Reading is not studying
> Memorizing 690 answers does not create confidence. Doing these three things does:

1. **Type every code sample.** The Integer cache trap sticks forever after you print it once; it never sticks from reading.
2. **Answer out loud.** Interviews are spoken. Silent recognition ≠ spoken explanation.
3. **Prepare stories, not just facts.** For each ⭐⭐ question, have one line from your own experience: "I hit this when…". That single sentence is what separates a memorizer from an engineer.

**Obsidian tips:**
- Blocks written as `> [!question]- ...` are **collapsed by default** — perfect for self-testing. Guess, then click to reveal.
- Use the tag `#java` in the graph view to see the whole map.
- The checklists at the end of each part are real checkboxes — tick them as you go. ✅

---

## 🔗 Recommended Next Steps

After this series, the natural extensions are:
- **Spring / Spring Boot** (DI, AOP, transactions, Spring MVC lifecycle)
- **SQL & JPA/Hibernate** (N+1 problem, lazy loading, transaction isolation)
- **System design** (caching, load balancing, database scaling)
- **Testing** (JUnit 5, Mockito, test doubles)
- **Books:** *Effective Java* (Bloch) and *Java Concurrency in Practice* (Goetz) — most of the deeper answers here trace back to these two.

---

> [!success] 690 questions · 9 parts · 1 goal
> Walk in knowing five topics cold rather than ninety topics vaguely. Good luck. 🍀

#java #interview #core-java #moc
