---
title: Checkpoints and Traps
type: support
tags:
  - roadmap
  - review
series: Java Data Engineering
---

# 🚧 Checkpoints & Traps

> Read the trap list **now**, before you start. Most people who fail this path do not fail on the technical content. They fail on one of the eight things below.

**Index:** [[06 - Java Data Engineering/00 - Overview|START HERE]]

---

## Self-tests

Answer out loud, in English, without notes. If you cannot, the phase is not finished — regardless of what the calendar says.

### End of [[06 - Java Data Engineering/01 - Phase 1 - Backend Foundation/00 - Overview|Phase 1 - Backend Foundation]]
1. Why did this query get slow after the table grew? *(with a query plan in front of you)*
2. What is the difference between `LEFT JOIN` and `INNER JOIN` in terms of **row counts**, and when does a join accidentally duplicate rows?
3. Write a window function query that returns the latest record per customer.
4. Your service is deployed and returning 500s. Walk me through your first five minutes.
5. What does `@Transactional` actually do, and what happens if you call a `@Transactional` method from inside the same class?
6. Explain your Dockerfile line by line and why it is in that order.

### End of [[06 - Java Data Engineering/02 - Phase 2 - Data Foundations/00 - Overview|Phase 2 - Data Foundations]]
1. What is the grain of your fact table, and why did you choose it?
2. When is SCD Type 2 correct and when is it a waste?
3. Why is columnar storage faster for analytics? Explain it to a non-engineer.
4. How do you make a load idempotent?
5. A source added a column overnight. What happens to your pipeline, and what *should* happen?
6. Why not just run the reports against the production database?

### End of [[06 - Java Data Engineering/03 - Phase 3 - Pipelines and Distributed Systems/00 - Overview|Phase 3 - Pipelines and Distributed Systems]]
1. A consumer crashes after processing 500 of 1000 messages but before committing the offset. What happens? How did you design so that it is safe?
2. Your Spark job is slow. Give me your diagnostic order.
3. What is data skew and how do you fix it?
4. When would you choose batch over streaming — and argue *for* batch convincingly.
5. Backfill 6 months of a broken pipeline. What could go wrong?
6. How do you know your data is correct today, without a human checking?

### End of [[06 - Java Data Engineering/04 - Phase 4 - Production and Seniority/00 - Overview|Phase 4 - Production and Seniority]]
1. Design a data platform for [a business you have never worked in]. Ask me the right questions first.
2. What are your SLOs and why those numbers?
3. Something broke and the CEO saw a wrong number. Walk me through the incident and the postmortem.
4. What technology in your platform would you remove, and why?
5. How would you cut this platform's cost by 40%?

---

## The eight traps

### 1. Tutorial hell
Watching feels like learning. It is not. **70% building, 20% reading, 10% watching.** If you finished a course and built nothing, you learned nothing that survives a month.

### 2. Tool collecting
"I know Airflow, Kafka, Spark, dbt, Flink, Snowflake…" — knowing the names of tools is worth nothing. Depth in three tools beats surface in fifteen. The interview question is never *"have you used X?"*, it is *"why did you choose X, and what did it cost you?"*

### 3. The analyst detour
Taking a data analyst job because it is easier to get, then discovering three years later that hiring managers read you as the dashboard person, your salary is anchored low, and the engineering door is harder to open than it was on day one. If you must take it as a door — **push toward pipelines, code and infrastructure from week one**, not toward prettier charts.

### 4. The consultancy typecast
Five years of writing the same CRUD service for different clients, with no ownership, no production operation, no design decisions. It feels like experience. It is one year repeated five times. **Test yourself every year: what did I learn this year that I did not know last year?** If the answer is thin, move.

### 5. Waiting until you are "ready"
You will never feel ready. **Apply for the data engineer role at the end of Phase 2**, not the end of Phase 4. Being paid to learn Phase 3 is faster than learning it alone, every single time.

### 6. Restarting
The most expensive habit in this whole document. Every 6 months a new field looks shinier — Go, Rust, AI agents, whatever is loud that month. Switching resets your depth to zero. **Five beginnings and zero depth is the most common way people lose in this field.** It is not caused by picking the wrong technology.

### 7. Skipping the boring layer
Linux, SQL, testing, Git, networking. Unglamorous, and they are the actual foundation. People who skip these hit a hard ceiling at mid-level and never understand why.

### 8. Learning in private
Nobody can hire what they cannot see. Especially across a border. **Public repos, public writing, public contributions.** See [[06 - Java Data Engineering/06 - Iran Playbook|Iran Playbook]].

---

## Review rhythm

**Weekly (10 minutes, Friday)**
- Update checkboxes
- One line in the progress log in [[06 - Java Data Engineering/00 - Overview|START HERE]]
- Is the current week's work moving the current phase forward, or am I drifting?

**Monthly (1 hour)**
- Is my building/reading/watching ratio still right?
- Am I stuck on something and hiding it by doing easier tasks instead?
- One paragraph written in English about something I learned

**Every 6 months (half a day) — the honest review**
- Am I ahead of, on, or behind the phase estimate — and *why*?
- What did I learn in these 6 months that I did not know before? Be specific.
- Is my current job still teaching me something?
- Am I visible? New public work in the last 6 months — yes or no?
- **The exit question:** if I am still in the exact same position in 12 months, is that acceptable?

---

## The deadline that protects you

Set a real date. Write it here:

**By [DATE + 24 months] I will either:**
- have a job title containing "Data" or "Platform", **or**
- have a written, specific reason why not — and a changed plan with a new date

Not a vague feeling. A date, in this note, that you look at every six months.

Drifting is the failure mode. Not Java. Not data science. **Drifting.**
