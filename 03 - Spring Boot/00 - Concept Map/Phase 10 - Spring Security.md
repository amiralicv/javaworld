---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 21
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🌱 Phase 10 — Spring Security

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/Phase 09 - Testing|Phase 9 — Testing (learn this earlier than you want to)]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/Phase 11 - Production - Observability & Operations|Phase 11 — Production: Observability & Operations]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **181. Authentication vs authorization** 🔴 — who you are vs what you may do.
- [ ] **182. The security filter chain** 🔴 — security is a chain of servlet filters running before your controller. Everything else follows from this.
- [ ] **183. `SecurityFilterChain` bean configuration** 🔴 — the modern lambda DSL config style (`WebSecurityConfigurerAdapter` is gone).
- [ ] **184. `SecurityContext` & `Authentication`** 🔴 — where the current user lives and how to read it.
- [ ] **185. `UserDetails` / `UserDetailsService`** 🔴 — loading users from your own store.
- [ ] **186. `PasswordEncoder` / BCrypt** 🔴 — never store plain or simply hashed passwords.
- [ ] **187. `AuthenticationManager` / `AuthenticationProvider`** 🟡 — the pluggable authentication engine.
- [ ] **188. HTTP Basic and form login** 🟡.
- [ ] **189. Sessions vs stateless (token) authentication** 🔴 — and why REST APIs usually go stateless.
- [ ] **190. CSRF** 🔴 — what the attack is, why it matters for cookies, why it is disabled for token APIs.
- [ ] **191. Authorization rules by URL** 🔴 — `requestMatchers().hasRole()`, order matters.
- [ ] **192. Method security** 🔴 — `@PreAuthorize`, `@PostAuthorize`, `@Secured`, SpEL in expressions.
- [ ] **193. Roles vs authorities** 🔴 — the `ROLE_` prefix trap.
- [ ] **194. JWT** 🔴 — structure, signature, expiry, refresh tokens, and why you cannot revoke a plain JWT easily.
- [ ] **195. OAuth2 & OpenID Connect concepts** 🟡 — grant types, tokens, the four roles.
- [ ] **196. OAuth2 client (login with Google/GitHub)** 🟡.
- [ ] **197. Resource server (validating tokens)** 🟡.
- [ ] **198. Authorization server** 🟢 — issuing tokens yourself.
- [ ] **199. CORS + security interaction** 🟡 — the order of filters explains most "it works with curl but not the browser" bugs.
- [ ] **200. Security headers & common attacks** 🟡 — XSS, clickjacking, HSTS, injection, mass assignment.
- [ ] **201. Custom filters and entry points** 🟡 — where to insert your own logic in the chain.

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
