---
type: hub
series: Spring Data JPA
tags: [spring-data-jpa, moc]
---

# 💾 Spring Data JPA

> [!abstract] 🧭 Navigation
> 🏠 [[00 - Home|Home]]

> [!info] 📖 What this track covers
> From relational theory and SQL up through JDBC, Hibernate, Spring Data repositories, performance tuning and transactions.

## 🗺️ Stages

| # | Stage | Roadmap stages | Topics |
|---|---|---|---|
| 01 | 🔄 [[04 - Spring Data JPA/01 - Database Theory, SQL & ACID/00 - Overview\|Database Theory, SQL & ACID]] | 0–3 | 10 |
| 02 | 📇 [[04 - Spring Data JPA/02 - Advanced SQL & Indexing/00 - Overview\|Advanced SQL & Indexing]] | 4–5 | 11 |
| 03 | 🔌 [[04 - Spring Data JPA/03 - JDBC & Connection Pooling/00 - Overview\|JDBC & Connection Pooling]] | 6–7 | 10 |
| 04 | 🗃️ [[04 - Spring Data JPA/04 - ORM Theory & Hibernate Architecture/00 - Overview\|ORM Theory & Hibernate Architecture]] | 8–9 | 11 |
| 05 | 🧩 [[04 - Spring Data JPA/05 - Entity Mapping/00 - Overview\|Entity Mapping]] | 10 | 9 |
| 06 | 🧩 [[04 - Spring Data JPA/06 - Relationships & Associations/00 - Overview\|Relationships & Associations]] | 11 | 9 |
| 07 | 📦 [[04 - Spring Data JPA/07 - Repositories & Queries/00 - Overview\|Repositories & Queries]] | 12–13 | 13 |
| 08 | 🔄 [[04 - Spring Data JPA/08 - Performance & Transactions/00 - Overview\|Performance & Transactions]] | 14–15 | 13 |
| 09 | 🧪 [[04 - Spring Data JPA/09 - Auditing, Migrations & Testing/00 - Overview\|Auditing, Migrations & Testing]] | 16–17 | 11 |
| 10 | 🏗️ [[04 - Spring Data JPA/10 - Project Ladder/00 - Overview\|Project Ladder]] | 18 | 6 |

> [!tip] 🎯 How to work through it
> 1. Open a stage, then a topic note.
> 2. Learn → write **📝 My Notes** in your own words → write **💻 Code**.
> 3. Tick boxes only when you can explain them out loud. Update `status` as you go.

## 📊 Progress

```base
filters:
  and:
    - 'file.inFolder("04 - Spring Data JPA")'
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
