---
type: topic
series: Spring Security
stage: "01 - Fundamentals & Core Architecture"
status: todo
items: 48
created: 2026-09-28
tags: [spring-security, topic]
---

# 🔐 Stage 5 — Spring Security core architecture (the heart)

> [!abstract] 🧭 Navigation
> ⬅️ [[05 - Spring Security/01 - Fundamentals & Core Architecture/Stage 4 - The Servlet layer|Stage 4 — The Servlet layer (the ground Spring Security stands on)]] · 🔼 [[05 - Spring Security/01 - Fundamentals & Core Architecture/00 - Overview|01 - Fundamentals & Core Architecture]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] 5.1 What `spring-boot-starter-security` does automatically when you add it
- [ ] 5.2 The default generated password in the startup log and why it exists
- [ ] 5.3 **`springSecurityFilterChain`** — the single registered filter
- [ ] 5.4 **`FilterChainProxy`** — the real entry point that holds all security filters
- [ ] 5.5 **`SecurityFilterChain`** — a matcher + an ordered list of filters
- [ ] 5.6 How multiple `SecurityFilterChain` beans work and how the **first match wins**
- [ ] 5.7 `securityMatcher()` — restricting a chain to certain URLs
- [ ] 5.8 The standard filter order (memorize the main ones):
- [ ] 5.9 → `DisableEncodeUrlFilter`
- [ ] 5.10 → `WebAsyncManagerIntegrationFilter`
- [ ] 5.11 → `SecurityContextHolderFilter`
- [ ] 5.12 → `HeaderWriterFilter`
- [ ] 5.13 → `CorsFilter`
- [ ] 5.14 → `CsrfFilter`
- [ ] 5.15 → `LogoutFilter`
- [ ] 5.16 → `UsernamePasswordAuthenticationFilter`
- [ ] 5.17 → `RequestCacheAwareFilter`
- [ ] 5.18 → `SecurityContextHolderAwareRequestFilter`
- [ ] 5.19 → `AnonymousAuthenticationFilter`
- [ ] 5.20 → `SessionManagementFilter`
- [ ] 5.21 → `ExceptionTranslationFilter`
- [ ] 5.22 → `AuthorizationFilter` (last)
- [ ] 5.23 **`SecurityContextHolder`** — where the current user is stored
- [ ] 5.24 `SecurityContextHolder` strategies: `MODE_THREADLOCAL`, `MODE_INHERITABLETHREADLOCAL`, `MODE_GLOBAL`
- [ ] 5.25 **`SecurityContext`** — the container object holding the `Authentication`
- [ ] 5.26 **`Authentication`** interface: `getPrincipal()`, `getCredentials()`, `getAuthorities()`, `isAuthenticated()`
- [ ] 5.27 The double life of `Authentication`: request object (unauthenticated) → result object (authenticated)
- [ ] 5.28 **`GrantedAuthority`** and `SimpleGrantedAuthority`
- [ ] 5.29 **`AuthenticationManager`** — the contract for "authenticate this"
- [ ] 5.30 **`ProviderManager`** — the default implementation that delegates
- [ ] 5.31 **`AuthenticationProvider`** — one strategy per authentication type
- [ ] 5.32 The `supports(Class)` method and how `ProviderManager` picks a provider
- [ ] 5.33 Parent `AuthenticationManager` and provider hierarchies
- [ ] 5.34 **`UserDetails`** — the user model Spring Security understands
- [ ] 5.35 `UserDetails` flags: `isEnabled`, `isAccountNonExpired`, `isAccountNonLocked`, `isCredentialsNonExpired`
- [ ] 5.36 **`UserDetailsService`** — one method: `loadUserByUsername`
- [ ] 5.37 `UsernameNotFoundException` and why it should not leak information
- [ ] 5.38 **`PasswordEncoder`** — the hashing contract
- [ ] 5.39 **`DaoAuthenticationProvider`** — how `UserDetailsService` + `PasswordEncoder` combine
- [ ] 5.40 **`AuthenticationEntryPoint`** — what to do when _not authenticated_ (401)
- [ ] 5.41 **`AccessDeniedHandler`** — what to do when _authenticated but forbidden_ (403)
- [ ] 5.42 **`ExceptionTranslationFilter`** — converts security exceptions into 401 or 403
- [ ] 5.43 `AuthenticationException` vs `AccessDeniedException` — the 401/403 distinction
- [ ] 5.44 **`SecurityContextRepository`** — how the context is saved/loaded between requests
- [ ] 5.45 `HttpSessionSecurityContextRepository` vs `RequestAttributeSecurityContextRepository` vs `NullSecurityContextRepository`
- [ ] 5.46 The full request journey, end to end — draw it on paper from memory
- [ ] 5.47 Spring Security 6 changes vs 5: no `WebSecurityConfigurerAdapter`, lambda DSL only, `AuthorizationManager` replaces `AccessDecisionManager`
- [ ] 5.48 How to debug: `logging.level.org.springframework.security=TRACE` and reading the filter chain printout

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
