---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 16
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🌐 C. Web Layer — what the phases above missed

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/02 - Container & Configuration - what the phases above missed|B. Container & Configuration — what the phases above missed]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/04 - JPA & Hibernate - the biggest real gap in the phases above|D. JPA & Hibernate — the biggest real gap in the phases above]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **287. `HandlerMethodArgumentResolver`** 🟡 — inject your own custom object as a controller parameter (for example the current user). Very commonly needed, rarely taught.
- [ ] **288. `HandlerMethodReturnValueHandler`** 🟢 — the mirror image for return types.
- [ ] **289. `RequestBodyAdvice` / `ResponseBodyAdvice`** 🟡 — modify every request or response body globally (envelopes, masking, encryption).
- [ ] **290. Custom `HttpMessageConverter`** 🟢 — support a format Jackson does not handle.
- [ ] **291. Customizing the `ObjectMapper`** 🔴 — date formats, naming strategy, unknown-property behaviour, null handling. You will need this in every real project.
- [ ] **292. Date, time and time zones** 🔴 — `LocalDate` vs `Instant` vs `ZonedDateTime`, storing UTC, `@JsonFormat`. [Certain] A top-3 source of real bugs.
- [ ] **293. `BigDecimal` for money** 🔴 — never `double`. Scale and rounding mode matter.
- [ ] **294. `ErrorController` and the whitelabel error page** 🟡 — what Boot does when nothing handles the exception.
- [ ] **295. HTTP caching: ETag, `Cache-Control`, `Last-Modified`** 🟡 — plus `ShallowEtagHeaderFilter`.
- [ ] **296. Response compression and HTTP/2** 🟡 — a two-line config change with real impact.
- [ ] **297. Request size limits & multipart config** 🟡 — upload limits, temp file location.
- [ ] **298. Reading the request body twice** 🟡 — why it fails, and `ContentCachingRequestWrapper`.
- [ ] **299. Rate limiting / brute-force protection** 🟡 — filter-level or gateway-level; Bucket4j or Resilience4j.
- [ ] **300. Idempotency keys for POST** 🟡 — how clients retry safely.
- [ ] **301. Spring Session** 🟢 — sessions stored in Redis so multiple instances share them.
- [ ] **302. Sending email (`JavaMailSender`) + templated emails** 🟡.

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
