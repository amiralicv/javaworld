---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 16
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🧪 Phase 9 — Testing (learn this earlier than you want to)

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/Phase 08 - Data Access & Transactions|Phase 8 — Data Access & Transactions]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/Phase 10 - Spring Security|Phase 10 — Spring Security]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **165. Unit vs integration vs end-to-end** 🔴 — what each one buys you and costs you.
- [ ] **166. JUnit 5 + AssertJ** 🔴 — lifecycle annotations, parameterized tests, readable assertions.
- [ ] **167. Mockito** 🔴 — `mock`, `when/thenReturn`, `verify`, argument captors.
- [ ] **168. Testing without Spring** 🔴 — with constructor injection most service tests need no container at all. Fastest tests you will ever write.
- [ ] **169. `@SpringBootTest`** 🔴 — full context test; web environments (`MOCK`, `RANDOM_PORT`).
- [ ] **170. Test slices** 🔴 — `@WebMvcTest`, `@DataJpaTest`, `@JsonTest`, `@RestClientTest`, `@JdbcTest`. Load only the part you test.
- [ ] **171. `MockMvc`** 🔴 — call controllers without a real server.
- [ ] **172. `@MockitoBean` / `@MockBean`** 🔴 — replace a bean in the context with a mock.
- [ ] **173. `TestRestTemplate` / `WebTestClient`** 🟡 — real HTTP against a running test server.
- [ ] **174. `@TestConfiguration`** 🟡 — test-only beans.
- [ ] **175. Test context caching & `@DirtiesContext`** 🟡 — why your suite is slow and how to keep it fast.
- [ ] **176. `@ActiveProfiles`, test properties, `@TestPropertySource`** 🟡.
- [ ] **177. Testcontainers** 🔴 — real Postgres/Kafka/Redis in Docker for tests. H2 lies to you about SQL behaviour.
- [ ] **178. Spring Security test support** 🟡 — `@WithMockUser`, security-aware MockMvc.
- [ ] **179. WireMock / MockWebServer** 🟡 — faking external HTTP services.
- [ ] **180. Test data strategy** 🟡 — builders, fixtures, cleanup, transactional rollback in tests.

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
