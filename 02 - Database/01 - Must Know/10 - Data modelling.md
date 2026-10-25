---
type: topic
series: Database
stage: "01 - Must Know"
status: todo
items: 13
created: 2026-09-28
tags: [database, topic]
---

# 🧩 J. Data modelling

> [!abstract] 🧭 Navigation
> ⬅️ [[02 - Database/01 - Must Know/09 - Indexes - this belongs in tier 1, not later|I. Indexes — this belongs in tier 1, not later]] · 🔼 [[02 - Database/01 - Must Know/00 - Overview|01 - Must Know]] · ➡️ [[02 - Database/01 - Must Know/11 - Postgres in practice|K. Postgres in practice]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **88. Entity–relationship thinking** — entities, attributes, relationships, before any SQL.
- [ ] **89. Relationship types** — one-to-one, one-to-many, many-to-many with a junction table.
- [ ] **90. Normalization: 1NF, 2NF, 3NF** — in practice: no repeating groups, no partial dependency, no transitive dependency. Aim for 3NF by default.
- [ ] **91. Deliberate denormalization** — done for a measured read problem, never because normalizing "felt hard".
- [ ] **92. Surrogate vs natural keys** — the ID column versus a real-world identifier. Most of the time: surrogate.
- [ ] **93. `bigint` identity vs UUID** — sequential IDs are compact and index-friendly; UUIDs are distributed-friendly but hurt index locality (look at UUIDv7 as the compromise).
- [ ] **94. `SERIAL` vs `GENERATED ... AS IDENTITY`** — identity is the modern standard.
- [ ] **95. Sequences** — how they work, why gaps are normal and harmless.
- [ ] **96. Naming conventions** — pick one (snake_case, singular or plural, `_id` suffixes) and never mix.
- [ ] **97. Audit columns** — `created_at`, `updated_at`, `created_by`. Add them from day one.
- [ ] **98. Soft delete** — a `deleted_at` column changes *every* query and every unique constraint. Understand the cost before choosing it.
- [ ] **99. Storing money, quantities and units** — integer minor units or `numeric`, and store the currency.
- [ ] **100. Choosing what belongs in JSONB vs columns** — structured, queried, constrained data goes in columns. JSONB is for genuinely variable shapes.

## 📝 My Notes

> [!note] ✍️ In your own words
> What is it? Why does it exist? When should you **not** use it?

## 💻 Code

```sql
// minimal working example
```

## ⚠️ Gotchas & Traps

-

## ❓ Self-Test

- [ ] I can explain this out loud in 2 minutes without notes
- [ ] I wrote working code for it without copying

## 🔗 Related

-
