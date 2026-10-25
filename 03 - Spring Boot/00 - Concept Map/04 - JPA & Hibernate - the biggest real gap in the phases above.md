---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 20
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🗃️ D. JPA & Hibernate — the biggest real gap in the phases above

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/03 - Web Layer - what the phases above missed|C. Web Layer — what the phases above missed]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/05 - Security - what the phases above missed|E. Security — what the phases above missed]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **303. `equals()` and `hashCode()` on entities** 🔴 — [Certain] the most damaging quiet bug in Spring apps. Never use Lombok `@Data`/`@EqualsAndHashCode` on an entity; a generated ID is null before persist, so the object breaks inside `HashSet` and the persistence context.
- [ ] **304. Lombok on entities in general** 🔴 — `@ToString` triggers lazy loading and can print your whole database. `@Data` generates setters you did not want.
- [ ] **305. Inheritance strategies** 🟡 — `SINGLE_TABLE`, `JOINED`, `TABLE_PER_CLASS`, and `@MappedSuperclass`. Different performance and schema shape.
- [ ] **306. Composite keys** 🟡 — `@EmbeddedId` vs `@IdClass`.
- [ ] **307. `@ElementCollection`** 🟡 — collections of value objects without a full entity.
- [ ] **308. `AttributeConverter`** 🟡 — map a custom type (or an encrypted column) to a database column.
- [ ] **309. Enum mapping** 🔴 — `EnumType.STRING`, always. `ORDINAL` breaks the moment someone reorders the enum.
- [ ] **310. `getReferenceById` vs `findById`** 🟡 — a lazy proxy versus a real select; useful for setting a foreign key without loading the row.
- [ ] **311. `save()` on an existing entity** 🟡 — it is a merge, and often an extra select you did not need. Dirty checking usually makes `save()` unnecessary.
- [ ] **312. Batch inserts and `saveAll` performance** 🟡 — needs `hibernate.jdbc.batch_size` and an ID strategy that does not force a select per row.
- [ ] **313. ID generation strategies** 🔴 — `IDENTITY` disables batching, `SEQUENCE` allows it, UUIDs cost index locality.
- [ ] **314. Second-level cache & query cache** 🟢 — powerful and easy to misuse.
- [ ] **315. Soft deletes** 🟡 — `@SQLDelete`, `@SQLRestriction`, and why a `deleted` flag complicates every query.
- [ ] **316. Flush modes and when Hibernate writes** 🟡 — before a query, before commit; explains surprising SQL ordering.
- [ ] **317. `open-in-view`** 🔴 — Boot enables it by default; it hides `LazyInitializationException` and holds connections during view rendering. [Likely] you should turn it off and fix the real cause.
- [ ] **318. Reading the generated SQL** 🔴 — `show-sql`, formatted SQL, statistics, or a tool like p6spy. You cannot tune what you cannot see.
- [ ] **319. Connection pool sizing** 🔴 — bigger is not better; pool size interacts with DB max connections and thread count.
- [ ] **320. Read replicas & routing datasources** 🟢 — sending reads elsewhere.
- [ ] **321. Multi-tenancy** 🟢 — schema-per-tenant, discriminator column, database-per-tenant.
- [ ] **322. Testing SQL against the real database** 🔴 — H2 accepts SQL that Postgres rejects. This is why Testcontainers exists.

## 📝 My Notes

> [!note] ✍️ In your own words
> What is it? Why does it exist? When should you **not** use it?

## 💻 Code

```java
// minimal working example
```

## ⚠️ Gotchas & Traps

-

## ❓ Self-Test

- [ ] I can explain this out loud in 2 minutes without notes
- [ ] I wrote working code for it without copying

## 🔗 Related

-
