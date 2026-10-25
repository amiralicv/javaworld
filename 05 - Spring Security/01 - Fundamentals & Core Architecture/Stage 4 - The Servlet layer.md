---
type: topic
series: Spring Security
stage: "01 - Fundamentals & Core Architecture"
status: todo
items: 13
created: 2026-09-28
tags: [spring-security, topic]
---

# 🌐 Stage 4 — The Servlet layer (the ground Spring Security stands on)

> [!abstract] 🧭 Navigation
> ⬅️ [[05 - Spring Security/01 - Fundamentals & Core Architecture/Stage 3 - Web security threats|Stage 3 — Web security threats (know the enemy first)]] · 🔼 [[05 - Spring Security/01 - Fundamentals & Core Architecture/00 - Overview|01 - Fundamentals & Core Architecture]] · ➡️ [[05 - Spring Security/01 - Fundamentals & Core Architecture/Stage 5 - Spring Security core architecture|Stage 5 — Spring Security core architecture (the heart)]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] 4.1 Servlet container basics (Tomcat) and the servlet lifecycle
- [ ] 4.2 `HttpServletRequest` and `HttpServletResponse`
- [ ] 4.3 **Filter** interface and `doFilter(request, response, chain)`
- [ ] 4.4 **FilterChain** — how filters pass control forward and back
- [ ] 4.5 Filter order and why order decides behavior
- [ ] 4.6 The difference between a Filter and a Spring MVC Interceptor
- [ ] 4.7 Filters run **before** `DispatcherServlet` — the key mental model
- [ ] 4.8 `HttpSession`, `JSESSIONID`, and how the container tracks sessions
- [ ] 4.9 Request attributes vs session attributes vs request parameters
- [ ] 4.10 `ThreadLocal` — one variable per request thread
- [ ] 4.11 Why `ThreadLocal` breaks with `@Async`, thread pools, and virtual threads
- [ ] 4.12 `DelegatingFilterProxy` — bridge from servlet container to Spring beans
- [ ] 4.13 `FilterRegistrationBean` and registering filters in Spring Boot

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
