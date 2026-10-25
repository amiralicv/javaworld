---
type: topic
series: Spring Security
stage: "01 - Fundamentals & Core Architecture"
status: todo
items: 25
created: 2026-09-28
tags: [spring-security, topic]
---

# 📚 Stage 1 — Security fundamentals (no framework, pure theory)

> [!abstract] 🧭 Navigation
> ⬅️ [[05 - Spring Security/01 - Fundamentals & Core Architecture/Stage 0 - Prerequisites|Stage 0 — Prerequisites (do not skip)]] · 🔼 [[05 - Spring Security/01 - Fundamentals & Core Architecture/00 - Overview|01 - Fundamentals & Core Architecture]] · ➡️ [[05 - Spring Security/01 - Fundamentals & Core Architecture/Stage 2 - Cryptography for developers|Stage 2 — Cryptography for developers (only what you need)]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] 1.1 What "security" means in software: protecting data, actions, and identity
- [ ] 1.2 The CIA triad: Confidentiality, Integrity, Availability
- [ ] 1.3 **Authentication** (who are you?) vs **Authorization** (what may you do?)
- [ ] 1.4 **Identification** vs authentication — a username is a claim, not proof
- [ ] 1.5 **Principal** — the entity being authenticated (user, service, device)
- [ ] 1.6 **Credentials** — the proof (password, token, certificate, biometric)
- [ ] 1.7 **Authority / Permission** — a single allowed action (`READ_INVOICE`)
- [ ] 1.8 **Role** — a named group of authorities (`ROLE_ADMIN`)
- [ ] 1.9 Role-Based Access Control (RBAC)
- [ ] 1.10 Attribute-Based Access Control (ABAC) and when RBAC is not enough
- [ ] 1.11 Access Control List (ACL) — permission per object, not per type
- [ ] 1.12 Principle of Least Privilege
- [ ] 1.13 Defense in Depth — never trust one single protection layer
- [ ] 1.14 Fail-secure / fail-closed — when unsure, deny
- [ ] 1.15 Trust boundary — where untrusted input crosses into your system
- [ ] 1.16 Threat modeling basics and the STRIDE categories
- [ ] 1.17 Attack surface — how each new endpoint increases risk
- [ ] 1.18 Statefulness vs statelessness in authentication
- [ ] 1.19 **Session** — server remembers you between requests
- [ ] 1.20 **Token** — the request carries its own proof
- [ ] 1.21 Multi-factor authentication (MFA/2FA) concept: something you know / have / are
- [ ] 1.22 Single Sign-On (SSO) concept
- [ ] 1.23 Federated identity and Identity Provider (IdP) vs Service Provider (SP)
- [ ] 1.24 Auditing and non-repudiation — proving who did what
- [ ] 1.25 Security vs usability trade-off — every control has a cost

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
