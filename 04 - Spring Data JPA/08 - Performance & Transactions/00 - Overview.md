---
type: stage
series: Spring Data JPA
topics: 13
tags: [spring-data-jpa, roadmap]
---

# 💾 Performance & Transactions

> [!abstract] 🧭 Navigation
> ⬅️ [[04 - Spring Data JPA/07 - Repositories & Queries/00 - Overview|07 - Repositories & Queries]] · 🏠 [[04 - Spring Data JPA/00 - Overview|Spring Data JPA]] · ➡️ [[04 - Spring Data JPA/09 - Auditing, Migrations & Testing/00 - Overview|09 - Auditing, Migrations & Testing]]

> Stages 14–15: Hibernate performance (N+1, caching, fetching strategies) and transactions in Spring. [Likely] this is the highest-leverage part of the whole roadmap — most "Hibernate is slow" complaints trace back to Stage 14, and most "why did my data not save / save twice" bugs trace back to Stage 15.

---

## Stage 14 — Hibernate performance: N+1, caching, fetch strategies

- ⚡ [[04 - Spring Data JPA/08 - Performance & Transactions/14.1 The N+1 select problem|14.1 The N+1 select problem]] · `0/6`
- ⚡ [[04 - Spring Data JPA/08 - Performance & Transactions/14.2 Fixing N+1 - the main techniques|14.2 Fixing N+1 — the main techniques]] · `0/12`
- ⚡ [[04 - Spring Data JPA/08 - Performance & Transactions/14.3 Fetch mode details|14.3 Fetch mode details]] · `0/4`
- ⚡ [[04 - Spring Data JPA/08 - Performance & Transactions/14.4 Second-level cache|14.4 Second-level cache]] · `0/13`
- 💾 [[04 - Spring Data JPA/08 - Performance & Transactions/14.5 Batch processing at scale|14.5 Batch processing at scale]] · `0/6`
- ⚡ [[04 - Spring Data JPA/08 - Performance & Transactions/14.6 Monitoring performance continuously|14.6 Monitoring performance continuously]] · `0/3`

---

## Stage 15 — Transactions in Spring

- 🔄 [[04 - Spring Data JPA/08 - Performance & Transactions/15.1 @Transactional fundamentals|15.1 `@Transactional` fundamentals]] · `0/7`
- 💾 [[04 - Spring Data JPA/08 - Performance & Transactions/15.2 Propagation|15.2 Propagation]] · `0/10`
- 🔄 [[04 - Spring Data JPA/08 - Performance & Transactions/15.3 Isolation at the Spring level|15.3 Isolation at the Spring level]] · `0/3`
- 💾 [[04 - Spring Data JPA/08 - Performance & Transactions/15.4 Rollback rules|15.4 Rollback rules]] · `0/6`
- 💾 [[04 - Spring Data JPA/08 - Performance & Transactions/15.5 Timing and boundary pitfalls|15.5 Timing and boundary pitfalls]] · `0/8`
- 🔄 [[04 - Spring Data JPA/08 - Performance & Transactions/15.6 Long transactions and their costs|15.6 Long transactions and their costs]] · `0/4`
- 🧪 [[04 - Spring Data JPA/08 - Performance & Transactions/15.7 Testing transactional code|15.7 Testing transactional code]] · `0/4`

---

---

## 📊 Progress

> [!tip] Set `status: learning` when you start a topic and `status: done` when every box is ticked.

```base
filters:
  and:
    - 'file.inFolder("04 - Spring Data JPA/08 - Performance & Transactions")'
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
