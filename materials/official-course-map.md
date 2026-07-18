# learn-dataops-with-phoebe - official course map

Two-track course. Leader track (a1-a6, 6 x 45 min, no code) + Builder track (b1-b8, 8 x 45 min, running project **RetailPulse**). Stack: OSS core (Git, GitHub Actions, Docker, Airflow, dbt, Great Expectations, MLflow, Flyway/Alembic, Evidently) with AWS/Databricks mapping sidebars.

**Theme:** Pipeline Slate x Flow-Teal x Signal-Amber. Attribution: by Phoebe Fu. Hyphen only, never em/en dash.

**Re-verify before delivery:** tool version numbers and cloud service names move fast - check changelogs (Airflow, dbt, MLflow, GitHub Actions runner images) near delivery date.

---

## What DataOps is (the spine every session hangs on)

DataOps = DevOps discipline + Agile + lean manufacturing, applied to the whole data+ML+DB lifecycle. Goal: ship data/ML changes fast, safely, repeatably, with quality gates - the same way DevOps industrialized software delivery. Four pillars:

1. **DevOps basics** - version control, CI/CD, IaC, containers, pipelines-as-code
2. **Data CI/CD** - orchestration (Airflow/Dagster), data testing (dbt tests / Great Expectations), data contracts, quality gates
3. **MLOps** - experiment tracking, model registry, model CI/CD, drift monitoring, retraining
4. **DBOps** - schema migrations, DB versioning, DB CI/CD, safe rollback

Cross-cutting: observability, secrets, environment promotion (dev -> staging -> prod).

---

## Running project - RetailPulse (builder track)

One repo grows across 8 sessions. A retail sales data product: raw sales CSV -> cleaned parquet -> orchestrated pipeline -> tested + contracted -> loaded to Postgres with migrations -> demand-forecast model -> served + monitored -> full CD to prod.

| Session | RetailPulse state |
|---|---|
| b1 | v0.1 - repo scaffold, Git flow, pre-commit (black/ruff), GitHub Actions CI, Dockerfile, `pipeline.py` (CSV->parquet) + 1 pytest, green CI |
| b2 | v0.2 - pipeline wrapped in an Airflow DAG (extract/transform/load tasks), scheduled, config via env |
| b3 | v0.3 - Great Expectations suite + dbt-style tests, a data contract (schema + expectations), quality gate fails the PR on breach |
| b4 | v0.4 - loaded to Postgres, schema migrations (Flyway/Alembic) versioned + run in CI, rollback demo |
| b5 | v0.5 - demand-forecast model, MLflow tracking + model registry, model CI (train+eval on PR) |
| b6 | v0.6 - model served (FastAPI + Docker), drift monitoring (Evidently), retrain trigger |
| b7 | v0.7 - pipeline observability, freshness/volume alerts, secrets management, Docker Compose stands up the whole stack |
| b8 | v1.0 - staging->prod promotion, end-to-end release pipeline (data+model+db together), tag/release, capstone checklist |

---

## Leader track coverage (a1-a6)

| # | Session | Teaches (~80% of) | Ends with |
|---|---|---|---|
| a1 | Why DataOps | reliability tax, artisanal->industrialized data, the 3 lineages (DevOps+Agile+lean), what DataOps promises | questions to ask your data team |
| a2 | Four pillars = four business risks | DevOps / Data CI-CD / MLOps / DBOps each mapped to a $ risk; the pipeline mental model | risk-map exercise |
| a3 | Maturity model | 5-level DataOps maturity, DORA-for-data metrics (deploy freq, lead time, MTTR, change-fail rate -> data equivalents) | self-assessment scorecard |
| a4 | Build vs buy vs OSS | OSS stack vs managed (Databricks/Snowflake/AWS), platform strategy, TCO, the one-platform convergence bet | score-the-option exercise |
| a5 | Org design + culture | who owns what (central vs data mesh), data contracts as social tech, team topologies, breaking silos | ownership-map exercise |
| a6 | ROI + roadmap | the business case, metrics that matter, proving ROI to a board, a 90-day roadmap | 90-day plan |

---

## Builder track coverage (b1-b8)

| # | Session | Pillar | Teaches (~80% of) |
|---|---|---|---|
| b1 | Foundations & repo | DevOps basics | Git trunk-based flow, repo layout, pre-commit, GitHub Actions CI (lint+test), Docker, pipeline-as-code |
| b2 | Orchestration | Data CI/CD | Airflow (vs Dagster note), DAGs/tasks/schedules, idempotency, backfills, config/secrets, env separation |
| b3 | Data testing & contracts | Data CI/CD | Great Expectations, dbt tests, data contracts, quality gates in CI, freshness/volume/schema checks |
| b4 | DBOps & migrations | DBOps | schema migrations (Flyway/Alembic), versioned DB, migration in CI/CD, expand-contract, rollback |
| b5 | Experiment tracking | MLOps | MLflow tracking + model registry, reproducibility (seed/params), model CI (train+eval gate) |
| b6 | Model deploy & monitor | MLOps | FastAPI serving + Docker, model promotion, drift/data-quality monitoring (Evidently), retrain triggers |
| b7 | Observability & IaC | Cross | pipeline observability (logs/metrics/lineage), alerting on freshness/volume, secrets, Docker Compose / IaC |
| b8 | Full CD & capstone | Cross | environment promotion dev->staging->prod, end-to-end release, blue-green/canary for data+model, capstone |

Cloud sidebars every builder session: how the OSS piece maps to AWS (CodePipeline, MWAA, Glue, SageMaker, RDS/DMS, CloudWatch) and Databricks/Snowflake where relevant.

---

## Not covered by design (honest list)

- Deep Kubernetes / Terraform authoring (named, mapped, not taught line-by-line) -> deep-dive track candidate
- Specific vendor certifications (Databricks/AWS/Astronomer exams) - official, stay official
- Streaming/real-time (Kafka/Flink) beyond a concept mention - out of scope for v1
- Feature stores (Feast) - deep-dive candidate
- Full spec of any one orchestrator's API - we teach the mental model + the 20% you use daily; docs own the rest
