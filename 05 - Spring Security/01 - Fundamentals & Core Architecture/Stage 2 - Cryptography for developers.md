---
type: topic
series: Spring Security
stage: "01 - Fundamentals & Core Architecture"
status: todo
items: 22
created: 2026-09-28
tags: [spring-security, topic]
---

# 🔏 Stage 2 — Cryptography for developers (only what you need)

> [!abstract] 🧭 Navigation
> ⬅️ [[05 - Spring Security/01 - Fundamentals & Core Architecture/Stage 1 - Security fundamentals|Stage 1 — Security fundamentals (no framework, pure theory)]] · 🔼 [[05 - Spring Security/01 - Fundamentals & Core Architecture/00 - Overview|01 - Fundamentals & Core Architecture]] · ➡️ [[05 - Spring Security/01 - Fundamentals & Core Architecture/Stage 3 - Web security threats|Stage 3 — Web security threats (know the enemy first)]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] 2.1 Encoding vs Encryption vs Hashing — three different things, never mix them
- [ ] 2.2 Base64 is **encoding**, not security
- [ ] 2.3 Symmetric encryption (one shared key) — AES
- [ ] 2.4 Asymmetric encryption (public/private key pair) — RSA, ECDSA
- [ ] 2.5 Which key encrypts and which key decrypts, in each direction
- [ ] 2.6 Digital signature — sign with private key, verify with public key
- [ ] 2.7 Cryptographic hash function properties: one-way, deterministic, collision resistant
- [ ] 2.8 Why MD5 and SHA-1 are broken for security use
- [ ] 2.9 Why fast hashes (SHA-256) are **wrong** for passwords
- [ ] 2.10 **Salt** — stops rainbow tables, must be unique per user
- [ ] 2.11 **Pepper** — application-wide secret, stored outside the database
- [ ] 2.12 Work factor / cost factor — making hashing intentionally slow
- [ ] 2.13 Adaptive password hashing algorithms: bcrypt, scrypt, Argon2, PBKDF2
- [ ] 2.14 HMAC — hash + secret key, used to sign JWTs (HS256)
- [ ] 2.15 Random vs secure random (`SecureRandom`) and why it matters
- [ ] 2.16 Constant-time comparison and timing attacks
- [ ] 2.17 TLS/SSL handshake at a high level
- [ ] 2.18 Certificates, Certificate Authorities, and the chain of trust
- [ ] 2.19 Keystore vs truststore, `.jks` / `.p12` / PEM formats
- [ ] 2.20 Mutual TLS (mTLS) concept
- [ ] 2.21 Key rotation and secret management (env vars, Vault, AWS Secrets Manager)
- [ ] 2.22 What "never roll your own crypto" really means in practice

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
