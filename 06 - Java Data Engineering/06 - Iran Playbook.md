---
title: Iran Playbook
type: support
tags:
  - roadmap
  - iran
  - strategy
series: Java Data Engineering
---

# 🇮🇷 Iran Playbook

> This is the note that makes the roadmap real instead of generic. A plan copied from a US blog will not survive contact with your situation.

**Index:** [[06 - Java Data Engineering/00 - Overview|START HERE]]

---

## 1. The constraint, stated plainly

Major US cloud platforms (AWS, Azure, GCP, Oracle Cloud) restrict Iranian users under OFAC rules. Account-based features on GitHub, npm publishing, and the VS Code marketplace are restricted. Virtually all international payment processors are unavailable. Even some modern internet protocols are affected, so infrastructure is slower and older than elsewhere.

**Do not waste energy being angry at this. Design around it.**

### What this rules out
- Cloud-certification paths (AWS/Azure/GCP certs). **You cannot register, and the certificate is not the skill anyway.**
- Managed-service-first learning (Snowflake, BigQuery, Databricks, Redshift)
- Heavy GPU model training → this is the real reason ML engineering is hard from here
- Paid API-based projects and anything requiring an international card

### What it does NOT rule out
- Everything in this roadmap. Every single tool in Phases 1–4 is open source and self-hostable.

---

## 2. Your stack, chosen for your reality

| Global default (blocked/hard) | Your version (open source, self-hosted) |
|---|---|
| S3 | **MinIO** |
| Snowflake / BigQuery | **ClickHouse**, DuckDB |
| Databricks | **Spark** + **Iceberg** + **Trino** |
| Managed Kafka (MSK/Confluent) | **Kafka** self-hosted, or Redpanda |
| Glue / Data Factory | **Airflow** |
| dbt Cloud | **dbt-core** |
| CloudWatch / Datadog | **Prometheus + Grafana + Loki** |
| Looker / Power BI | **Metabase**, **Superset** |
| EKS / GKE | **k3s** on your own machines |

**Local providers** (Arvan, Liara and similar) exist for hosting when you need something outside your own laptop.

### The reframe

Someone in Berlin clicks "create managed Kafka cluster" and never learns what a broker is. **You will install it, break it, tune it, and fix it.** When both of you interview for the same senior role and the interviewer asks what happens during a consumer group rebalance, only one of you has actually watched it happen.

**Your constraint is your differentiator — but only if you self-host seriously instead of just watching videos about managed services you cannot use.**

Write this on your CV as a positive: *"Built and operated self-hosted data infrastructure (Kafka, Spark, Iceberg, Airflow, Kubernetes) end to end."* That sentence is rarer than any certificate.

---

## 3. Hardware

You need one decent machine. This is the main money you should spend on your career.

- **Minimum:** 16 GB RAM, 4+ cores, 500 GB SSD
- **Comfortable:** 32 GB RAM, 8 cores, 1 TB NVMe
- **Better than a new laptop:** a used server or an old desktop as a home lab. Two cheap machines beat one expensive one for learning distributed systems, because *distributed* needs more than one node.
- Run everything in Docker/k3s locally. Your whole Phase 3 platform can live on one 32 GB box.

---

## 4. English — the highest-return skill on this list

For an Iranian engineer, English is worth more than any framework. It is the visa, the remote job, the documentation, and the interview.

- [ ] **20 minutes daily, minimum.** Non-negotiable.
- [ ] Read official docs in English only. Never a translated tutorial.
- [ ] Write your commits, READMEs, and notes in English — including this vault
- [ ] Speaking is the weak point for most people here: talk to yourself explaining technical concepts out loud, record it, listen back. It is uncomfortable and it works.
- [ ] Aim for a real assessed level (IELTS/TOEFL band or equivalent) before you need it, not when you need it

**Test:** can you explain your Project D architecture out loud, in English, for 5 minutes, without notes? If not, that is a bigger blocker than any missing tool.

---

## 5. The local market

**Where the money is inside Iran**
- **Banking, core banking, and fintech** — heavy JVM usage, stable, and pays at the top of the local range. Your Java internship points directly here.
- **Insurance, telecom, government contractors** — same profile, slower, very stable
- **Large local tech companies** (e-commerce, ride-hailing, marketplaces, streaming) — the real data engineering work locally; they self-host at genuine scale
- **Consulting/outsourcing shops** — easy entry, but watch the typecasting risk in [[06 - Java Data Engineering/07 - Checkpoints and Traps|Checkpoints and Traps]]

**Realities to plan around**
- Junior backend salaries are modest; the increase with seniority is steep. Year one is about experience, not income.
- Currency inflation means a rising monthly salary can still be falling real income. **Measure your progress in portable skill, not in toman.**
- Frontend has more job ads but a lower ceiling and far more competition. Backend/data is thinner but scarcer.

**Where to look:** Jobinja, Jobvision, IranTalent, Quera, and — more effective than all of them — engineers you already know. Referrals beat applications everywhere, and especially in a small market.

---

## 6. Visibility across the border

You cannot walk into a foreign office. So build the things that travel without you:

- [ ] **Public repositories** with excellent READMEs. Public repos remain reachable even where account features are restricted.
- [ ] **A personal site** with your writing — self-hosted, your own domain if possible
- [ ] **Technical articles in English**, published consistently. This is the single strongest cross-border signal available to you.
- [ ] **Open source contributions** — small, useful, real. A merged PR to Airflow, dbt, or a Kafka connector is worth more than a portfolio of demos.
- [ ] A CV written for an international reader: outcomes, scale, and numbers. Not a tool list.

---

## 7. The exit / remote question — be realistic

The blocker for international work is **payment and compliance, not your skill.**

- Most Iranian engineers who reach international work **relocate first.** Germany, Netherlands, Turkey, UAE, Canada and Georgia are the common destinations.
- **Backend, data and platform engineers are the profiles companies sponsor.** Junior data scientists and analysts are not. This is a large part of why this roadmap targets data engineering.
- Academic routes (master's abroad) are a parallel path and work well for this field.
- Anything involving cross-border payment arrangements: **get proper legal and tax advice from a qualified professional before you do it.** Do not take career advice on that from the internet, including from me.

**Timeline honesty:** the profile that gets sponsored is mid-level, roughly the end of [[06 - Java Data Engineering/03 - Phase 3 - Pipelines and Distributed Systems/00 - Overview|Phase 3 - Pipelines and Distributed Systems]]. That is 2–3 years of serious work. Plan for that, not for a shortcut.

---

## 8. What to do when the internet is bad

It will be. Build for it instead of losing the day:

- [ ] Download docs for offline reading (devdocs-style offline sets, PDF copies of official docs)
- [ ] Keep a local mirror of the Docker images and packages you use often
- [ ] Buy real books; they never go down
- [ ] Keep a "no internet" task list: read source code you already cloned, write design docs, refactor, write articles, practice SQL against your local Postgres

**Rule:** a bad connection is a reading and writing day, not a lost day.
