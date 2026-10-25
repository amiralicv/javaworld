---
title: Portfolio Projects
type: support
tags:
  - roadmap
  - projects
series: Java Data Engineering
---

# 🏗️ Portfolio Projects

> **The rule:** five finished projects beat fifty started ones. A finished project has a README, tests, and something a stranger can run.
> Certificates prove attendance. Projects prove ability. Only one of those gets you hired from Iran.

**Index:** [[06 - Java Data Engineering/00 - Overview|START HERE]]

---

## What makes a project count

- [ ] **Real, ugly data.** Not a clean tutorial CSV. Real data has nulls, duplicates, wrong encodings, and a column that changes meaning halfway through.
- [ ] **It runs.** `docker compose up` and it works. Someone else can reproduce it.
- [ ] **It is tested.** At least the critical paths.
- [ ] **It is documented.** Architecture diagram, why you chose X over Y, what you would fix.
- [ ] **It handles failure.** What happens if the source is down? If the file arrives twice? If a column disappears?
- [ ] **It is public.** Public repo. In English.

**Data sources you can use:** government open data portals, Wikipedia dumps, OpenStreetMap, GitHub Archive, public transport data, weather data, cryptocurrency APIs, sports data, your own bank statements (scrubbed), scraped public sites you are allowed to scrape.

---

## Project A — Production-Style Backend Service
**Phase:** [[06 - Java Data Engineering/01 - Phase 1 - Backend Foundation/00 - Overview|Phase 1 - Backend Foundation]] · **Time:** 3–5 weeks

A Spring Boot service with a real domain (not "todo app"). Pick something with actual rules — inventory with reservations, a lending library with fines, a booking system with conflicts.

**Must include**
- REST API with validation and proper error responses
- Postgres with a considered schema and migrations (Flyway/Liquibase)
- Authentication
- Unit tests + integration tests with Testcontainers
- Dockerfile + docker compose
- Actuator health/metrics endpoint
- Deployed on a real Linux server behind nginx, running under systemd
- README with setup instructions and an API description

**The bar:** a stranger clones it and has it running in under 10 minutes.

---

## Project B — Messy File → Clean Database
**Phase:** Phase 1 (end) · **Time:** 2–3 weeks

Your first data pipeline, written in Java. Deliberately.

**Must include**
- Reads a large, dirty CSV/JSON source (100MB+, with real problems in it)
- Validates every row; rejects bad rows into a quarantine table **with the reason**
- Loads clean data into Postgres in batches
- **Idempotent:** run it 5 times, get the same result
- Resumable: if it crashes at row 400,000 it does not start from zero
- Logs a run summary: rows read, loaded, rejected, duration
- Tested with intentionally broken input files

**The lesson:** you will meet these same five problems in every pipeline for the rest of your career, no matter the tool.

---

## Project C — Batch Warehouse, End to End
**Phase:** [[06 - Java Data Engineering/02 - Phase 2 - Data Foundations/00 - Overview|Phase 2 - Data Foundations]] · **Time:** 6–8 weeks

The project that makes you employable as a junior data engineer.

**Architecture**
```
API / files  →  raw layer (Parquet on MinIO)
             →  cleaned layer (typed, deduplicated, validated)
             →  star schema (ClickHouse or Postgres)
             →  dashboard (Metabase or Superset, both self-hostable)
```

**Must include**
- 2+ different sources, joined into one model
- A documented star schema: fact table, dimensions, and **a written statement of the grain**
- At least one SCD Type 2 dimension
- Incremental loading with a watermark
- Python, typed and tested
- Data quality checks at each layer
- A README explaining the model **and the design you rejected**

**Add difficulty on purpose:** make one source change its schema halfway through the history. Handle it.

---

## Project D — Streaming + Batch Platform
**Phase:** [[06 - Java Data Engineering/03 - Phase 3 - Pipelines and Distributed Systems/00 - Overview|Phase 3 - Pipelines and Distributed Systems]] · **Time:** 3–4 months

The centerpiece. This is the one you talk about in interviews.

**Architecture**
```
Postgres ──Debezium CDC──┐
                          ├──> Kafka ──┬──> Flink/Kafka Streams ──> ClickHouse (real-time)
API poller ───────────────┘            └──> Spark batch ──> Iceberg on MinIO ──> Trino
                                              ↑
                                    Airflow orchestrates
                                    dbt transforms
                                    quality checks gate every load
```

**Must include**
- CDC from a live database (not a fake file drop)
- Schema Registry with a real schema evolution event
- Both a streaming path and a batch path over the same data — **and a written comparison of what each one is good for**
- Airflow DAGs that are idempotent and backfillable
- dbt models with tests and documentation
- Data quality gates that stop a bad load
- Alerting on failure
- Architecture diagram + design doc

**The bar:** you can kill any single component and explain exactly what is lost, what recovers by itself, and what needs a human.

---

## Project E — Platform on Kubernetes
**Phase:** [[06 - Java Data Engineering/04 - Phase 4 - Production and Seniority/00 - Overview|Phase 4 - Production and Seniority]] · **Time:** 3–4 months

Take Project D and make it operable by someone who is not you.

**Must include**
- Everything running on Kubernetes (k3s on your own machines is fine and is actually more impressive)
- Infrastructure as code — the whole thing rebuildable from an empty cluster
- Prometheus + Grafana with **meaningful** dashboards and alerts
- Defined SLOs for freshness and completeness
- Secrets management
- CI/CD pipeline that tests before deploy
- A runbook: "if X breaks at 3 AM, do this"
- A postmortem you wrote about something that actually broke

---

## Writing project (do this continuously)

Every phase, publish one technical article in English about something you learned deeply.

**Why this matters more than you think:** it proves English, proves depth, proves communication, and it is a portfolio that reaches people who cannot meet you. From Iran, a public body of written work is one of the strongest signals you can send across a border. See [[06 - Java Data Engineering/06 - Iran Playbook|Iran Playbook]].

Good topics: *"Why my Spark job was slow and the three things that fixed it." "How I implemented SCD Type 2 without dbt snapshots." "What actually happens when a Kafka consumer crashes mid-batch."*

Bad topics: *"Top 10 SQL commands."* Nobody needs that, and it proves nothing.
