---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 36
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🔄 Phase 8 — Data Access & Transactions

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/Phase 07 - Calling Other Services|Phase 7 — Calling Other Services (HTTP clients)]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/Phase 09 - Testing|Phase 9 — Testing (learn this earlier than you want to)]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **129. `DataSource` and connection pooling (HikariCP)** 🔴 — connections are expensive; pool size is a real tuning parameter.
- [ ] **130. `JdbcTemplate`** 🔴 — plain SQL without boilerplate.
- [ ] **131. `JdbcClient`** 🟡 — the modern fluent replacement for JdbcTemplate.
- [ ] **132. `RowMapper` / `ResultSetExtractor`** 🟡 — result set → object.
- [ ] **133. `NamedParameterJdbcTemplate`** 🟡 — named placeholders instead of `?`.
- [ ] **134. `DataAccessException` hierarchy & `@Repository`** 🟡 — vendor SQL exceptions translated into one consistent hierarchy.
- [ ] **135. Transaction fundamentals** 🔴 — ACID, commit, rollback; what a transaction actually guarantees.
- [ ] **136. `@Transactional`** 🔴 — declarative transaction boundaries.
- [ ] **137. Propagation** 🔴 — `REQUIRED`, `REQUIRES_NEW`, `NESTED`, `SUPPORTS`, `MANDATORY`, `NEVER`, `NOT_SUPPORTED`.
- [ ] **138. Isolation levels** 🟡 — read uncommitted → serializable; dirty read, non-repeatable read, phantom read.
- [ ] **139. Rollback rules** 🔴 — by default only unchecked exceptions roll back. Checked exceptions do not. Surprising and important.
- [ ] **140. `readOnly = true`** 🟡 — hints and real optimizations.
- [ ] **141. `@Transactional` pitfalls** 🔴 — self-invocation, private methods, wrong layer, transaction spanning HTTP calls, lazy loading after commit.
- [ ] **142. `PlatformTransactionManager` / `TransactionTemplate`** 🟡 — the programmatic API under the annotation.
- [ ] **143. ORM & JPA vs Hibernate** 🔴 — JPA is the specification, Hibernate is the implementation, Spring Data JPA is the convenience layer on top.
- [ ] **144. Entity mapping** 🔴 — `@Entity`, `@Table`, `@Id`, `@GeneratedValue`, `@Column`, `@Enumerated`, `@Embeddable`.
- [ ] **145. `EntityManager` & the persistence context** 🔴 — the first-level cache; the single biggest source of "why did my object change by itself".
- [ ] **146. Entity states** 🔴 — transient, managed, detached, removed.
- [ ] **147. Dirty checking & flush** 🔴 — changing a managed entity writes to the DB without any `save()`.
- [ ] **148. Relationships** 🔴 — `@OneToMany`, `@ManyToOne`, `@ManyToMany`, `@OneToOne`, owning side, `mappedBy`, cascade, orphan removal.
- [ ] **149. Fetch types: LAZY vs EAGER** 🔴 — default to LAZY, always.
- [ ] **150. N+1 select problem** 🔴 — the classic performance killer; fix with fetch joins, `@EntityGraph`, or batch size.
- [ ] **151. `LazyInitializationException`** 🔴 — accessing a lazy field outside the session; and why "open session in view" is a bad fix.
- [ ] **152. Spring Data JPA repositories** 🔴 — `Repository`, `CrudRepository`, `JpaRepository`; how an interface with no code gets an implementation.
- [ ] **153. Derived query methods** 🔴 — `findByEmailAndActiveTrue(...)` parsed from the method name.
- [ ] **154. `@Query`, JPQL and native SQL** 🔴.
- [ ] **155. `@Modifying` + queries that write** 🟡 — and why they need a transaction and can desync the persistence context.
- [ ] **156. Pagination & sorting** 🔴 — `Pageable`, `Page`, `Slice`, and why `Page` costs an extra count query.
- [ ] **157. Projections & DTO queries** 🔴 — select only what you need, interface or constructor projections.
- [ ] **158. `Specification` / Criteria API / QueryDSL** 🟡 — dynamic queries built at runtime.
- [ ] **159. Auditing** 🟡 — `@CreatedDate`, `@LastModifiedBy`, `@EnableJpaAuditing`.
- [ ] **160. Locking** 🟡 — optimistic (`@Version`) vs pessimistic; how to avoid lost updates.
- [ ] **161. Schema migration (Flyway / Liquibase)** 🔴 — versioned SQL migrations. `ddl-auto=update` is not a production strategy.
- [ ] **162. Multiple data sources** 🟢 — separate config, transaction managers, and the pain that follows.
- [ ] **163. Spring Data for NoSQL** 🟢 — MongoDB, Redis, Elasticsearch, Cassandra; same repository idea, different store.
- [ ] **164. Redis as cache and as store** 🟡.

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
