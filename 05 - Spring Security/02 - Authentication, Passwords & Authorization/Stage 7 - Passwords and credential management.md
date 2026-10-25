---
type: topic
series: Spring Security
stage: "02 - Authentication, Passwords & Authorization"
status: todo
items: 30
created: 2026-09-28
tags: [spring-security, topic]
---

# 🔑 Stage 7 — Passwords and credential management

> [!abstract] 🧭 Navigation
> ⬅️ [[05 - Spring Security/02 - Authentication, Passwords & Authorization/6.7 Authentication events|6.7 Authentication events]] · 🔼 [[05 - Spring Security/02 - Authentication, Passwords & Authorization/00 - Overview|02 - Authentication, Passwords & Authorization]] · ➡️ [[05 - Spring Security/02 - Authentication, Passwords & Authorization/8.1 Core authorization model|8.1 Core authorization model]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] 7.1 `PasswordEncoder` interface: `encode()`, `matches()`, `upgradeEncoding()`
- [ ] 7.2 `BCryptPasswordEncoder` — strength parameter, `$2a$` prefix, 72-byte limit
- [ ] 7.3 `Argon2PasswordEncoder` — memory, iterations, parallelism (and why it is the modern first choice)
- [ ] 7.4 `SCryptPasswordEncoder`
- [ ] 7.5 `Pbkdf2PasswordEncoder`
- [ ] 7.6 `NoOpPasswordEncoder` — deprecated, tests only, never production
- [ ] 7.7 **`DelegatingPasswordEncoder`** — the `{bcrypt}` / `{argon2}` prefix format
- [ ] 7.8 `PasswordEncoderFactories.createDelegatingPasswordEncoder()`
- [ ] 7.9 The `IllegalArgumentException: There is no PasswordEncoder mapped for the id "null"` error and its two fixes
- [ ] 7.10 Migrating an existing user table from one algorithm to another, with zero downtime
- [ ] 7.11 Choosing the right work factor: benchmark on your own production hardware
- [ ] 7.12 Password policy: length over complexity, and why forced rotation is discouraged now (NIST 800-63B)
- [ ] 7.13 Checking passwords against known-breach lists (Have I Been Pwned k-anonymity API)
- [ ] 7.14 Never log, never return, never store passwords in plain text — including in exception messages
- [ ] 7.15 Password reset flow design: single-use token, short expiry, hashed at rest, invalidate on use
- [ ] 7.16 Why password reset must not reveal whether the email exists
- [ ] 7.17 Change-password flow: require the current password, then invalidate other sessions
- [ ] 7.18 Spring Security's `/change-password` well-known endpoint support
- [ ] 7.19 `CompromisedPasswordChecker` and `HaveIBeenPwnedRestApiPasswordChecker` (Spring Security 6.3+)
- [ ] 7.20 Account lockout: threshold, duration, and the DoS risk of locking on username alone
- [ ] 7.21 Login rate limiting by IP + username combination
- [ ] 7.22 CAPTCHA integration as a step-up defense
- [ ] 7.23 One-Time Passwords: TOTP algorithm and how authenticator apps work
- [ ] 7.24 Spring Security 6.4+ built-in one-time-token login (`oneTimeTokenLogin()`)
- [ ] 7.25 Implementing a two-step MFA flow (partial authentication → OTP verification → full authentication)
- [ ] 7.26 Recovery codes for MFA
- [ ] 7.27 WebAuthn / Passkeys concept, and Spring Security 6.4+ `webAuthn()` support
- [ ] 7.28 API keys: generation, hashing at rest, prefix design, scoping, rotation
- [ ] 7.29 Storing secrets outside the codebase — env vars, config server, Vault
- [ ] 7.30 `Jasypt` / Spring Cloud Config encryption for property values

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
