---
type: topic
series: Spring Security
stage: "01 - Fundamentals & Core Architecture"
status: todo
items: 33
created: 2026-09-28
tags: [spring-security, topic]
---

# 🛡️ Stage 3 — Web security threats (know the enemy first)

> [!abstract] 🧭 Navigation
> ⬅️ [[05 - Spring Security/01 - Fundamentals & Core Architecture/Stage 2 - Cryptography for developers|Stage 2 — Cryptography for developers (only what you need)]] · 🔼 [[05 - Spring Security/01 - Fundamentals & Core Architecture/00 - Overview|01 - Fundamentals & Core Architecture]] · ➡️ [[05 - Spring Security/01 - Fundamentals & Core Architecture/Stage 4 - The Servlet layer|Stage 4 — The Servlet layer (the ground Spring Security stands on)]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] 3.1 The OWASP Top 10 — read it once fully, then return to it after Stage 12
- [ ] 3.2 HTTP is stateless — the root cause of session and token design
- [ ] 3.3 Cookies: `Domain`, `Path`, `Expires`, `Max-Age`
- [ ] 3.4 Cookie security flags: `HttpOnly`, `Secure`, `SameSite=Strict/Lax/None`
- [ ] 3.5 Same-Origin Policy (SOP) — what "origin" means (scheme + host + port)
- [ ] 3.6 CORS — why the browser blocks it and why CORS is **not** a security feature for your server
- [ ] 3.7 Preflight `OPTIONS` request and when it is triggered
- [ ] 3.8 **CSRF** — how it works, why cookies enable it, why tokens in headers usually don't
- [ ] 3.9 CSRF defenses: synchronizer token, double-submit cookie, `SameSite`
- [ ] 3.10 **XSS** — stored, reflected, DOM-based
- [ ] 3.11 Why XSS defeats `HttpOnly`-less token storage in `localStorage`
- [ ] 3.12 Output encoding and Content Security Policy (CSP)
- [ ] 3.13 **SQL Injection** and why parameterized queries fix it
- [ ] 3.14 Command injection, path traversal, and unsafe file upload
- [ ] 3.15 **Session fixation** attack
- [ ] 3.16 **Session hijacking** and token theft
- [ ] 3.17 Clickjacking and `X-Frame-Options` / `frame-ancestors`
- [ ] 3.18 MIME sniffing and `X-Content-Type-Options: nosniff`
- [ ] 3.19 **Broken Access Control** — the most common real-world bug
- [ ] 3.20 **IDOR** (Insecure Direct Object Reference) — `/orders/42` belongs to someone else
- [ ] 3.21 Privilege escalation: horizontal vs vertical
- [ ] 3.22 Mass assignment / over-posting
- [ ] 3.23 Brute force, credential stuffing, password spraying
- [ ] 3.24 Rate limiting and account lockout as defenses
- [ ] 3.25 User enumeration through error messages and response timing
- [ ] 3.26 Open redirect
- [ ] 3.27 **SSRF** (Server-Side Request Forgery)
- [ ] 3.28 Insecure deserialization
- [ ] 3.29 Security misconfiguration: default passwords, debug endpoints, verbose errors
- [ ] 3.30 Sensitive data exposure in logs, stack traces, and API responses
- [ ] 3.31 Dependency vulnerabilities and supply chain risk (CVE, `dependency-check`)
- [ ] 3.32 Replay attacks and nonces
- [ ] 3.33 Man-in-the-middle and why HTTPS everywhere is not optional

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
