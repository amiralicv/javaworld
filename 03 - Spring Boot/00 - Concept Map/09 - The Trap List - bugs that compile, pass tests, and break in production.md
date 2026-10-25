---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 24
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🧪 I. The Trap List — bugs that compile, pass tests, and break in production

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/08 - Tooling & Daily Workflow|H. Tooling & Daily Workflow]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/10 - Beliefs to unlearn|J. Beliefs to unlearn]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

Read this section twice. [Likely] you will meet at least six of these personally.

- [ ] **357. Self-invocation kills `@Transactional`, `@Cacheable`, `@Async`, `@PreAuthorize`** — calling `this.method()` bypasses the proxy. Silent, no error.
- [ ] **358. Checked exceptions do not roll back by default.**
- [ ] **359. Mutable state in a singleton bean** — works locally with one user, corrupts data under load.
- [ ] **360. Field injection hides missing dependencies** and makes plain unit tests impossible.
- [ ] **361. `@Transactional` on a method that calls an external HTTP API** — you hold a DB connection while waiting on the network.
- [ ] **362. No timeout on an HTTP client** — one slow dependency exhausts your threads and takes the whole service down.
- [ ] **363. N+1 queries** — fine with 10 rows in dev, fatal with 100,000 in prod.
- [ ] **364. `EAGER` fetching everywhere** — one query pulls half the database.
- [ ] **365. `ddl-auto=update` in production** — silent schema drift, no rollback, eventual data loss.
- [ ] **366. Exposing entities directly as API responses** — leaks fields, breaks the API on every schema change, causes lazy-loading errors during serialization.
- [ ] **367. Lombok `@Data` on JPA entities** — see item 303.
- [ ] **368. `@Scheduled` job running on every instance** — the job executes N times when you scale out.
- [ ] **369. Cache without an eviction strategy** — memory leak, or stale data forever.
- [ ] **370. Retrying a non-idempotent call** — duplicate charges, duplicate orders.
- [ ] **371. Storing local time instead of UTC** — breaks at the daylight-saving boundary.
- [ ] **372. Secrets in `application.properties` committed to git.**
- [ ] **373. `permitAll()` placed after a broader rule** — order in the security chain matters; you can open or lock everything by accident.
- [ ] **374. CSRF disabled "to make it work"** without understanding whether you are cookie-based or token-based.
- [ ] **375. Blocking call inside a reactive chain** — destroys the event loop and the whole point of WebFlux.
- [ ] **376. Default thread pool used for `@Async`** — unbounded queue, hidden memory growth.
- [ ] **377. Catching `Exception` and logging it without rethrowing** — the transaction commits a half-finished state.
- [ ] **378. `open-in-view` masking a design problem** — see item 317.
- [ ] **379. Testing with H2 while running Postgres** — different SQL dialect, different behaviour, false confidence.
- [ ] **380. Connection pool too small (or far too large)** — queueing at the pool looks exactly like a slow database.

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
