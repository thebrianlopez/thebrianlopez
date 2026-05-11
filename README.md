# Hi, I'm Brian

Staff Platform Engineer at [Grindr](https://github.com/blo-grindr) (NYSE: GRND). I own the cloud infrastructure for a platform serving 15M monthly active users across 190 countries — 8 AWS accounts, 5+ EKS clusters, GitOps via ArgoCD, and the internal tooling that keeps engineers from doing things manually.

On the side, I build the cloud backbone for [Farewell John](https://farewelljohn.com/demo/), a four-person startup helping families navigate end-of-life care.

---

## What I'm Building

### [perfgate](https://github.com/thebrianlopez/perfgate)
A CLI for statistical performance gating in CI. You define a benchmark, set a threshold, and it fails the build if you have introduced a regression. Simple contract, serious signal.

### [closed-loop-telemetry](https://github.com/thebrianlopez/closed-loop-telemetry)
A JSONL event bus for AI-augmented engineering workflows. When your system includes non-deterministic components — LLMs, fuzzy matchers, probabilistic classifiers — you need observability that accounts for that. This is a starting point.

### [org-identity-bootstrap](https://github.com/thebrianlopez/org-identity-bootstrap)
Terraform modules for wiring up GitHub + AWS + GCP identity federation from scratch. Zero static credentials. Designed to be the first thing you run in a new org.

### [aws-iam-patterns](https://github.com/thebrianlopez/aws-iam-patterns)
A reference library of IAM patterns worth keeping around. Least-privilege role compositions, cross-account trust setups, and the guardrails that catch mistakes before they reach production.

### [mcp-aws-inspector](https://github.com/thebrianlopez/mcp-aws-inspector)
An MCP server that surfaces AWS IAM and S3 introspection directly into AI coding assistants. Security context, in the tool that is already open.

---

## Farewell John — Architecture ([hersolutionsllc](https://github.com/hersolutionsllc))

Full-stack CTO/founding engineer for [farewelljohn.com](https://farewelljohn.com) — funeral home price transparency platform.

- **Read-only API + Airflow write pipeline** — Express/Node.js serves PostgreSQL reads only; all data ingestion (Google Places → Playwright crawler → OpenAI/Claude PDF parser → PostgreSQL) runs in Airflow DAGs. Hard separation enforced at the service boundary.
- **PostGIS max-radius cache** — Airflow populates zipcodes at 50-mile radius; API filters to any smaller radius from the same cache row using `ST_DWithin`. Zero redundant external API calls.
- **OrbStack VM mirrors production EC2 exactly** — `make orbstack-up` boots a local prod clone via cloud-init, GHCR image pull, and S3 secrets bootstrap. Engineers validate against the real stack before every deploy.
- **CloudFront maintenance-mode edge functions** — KVS-backed CF Functions return 503 at the edge without touching EC2. `/demo/*` always available. Zero-downtime maintenance window.
- **GitHub Actions OIDC → IAM nginx publishing** — nginx configs have a single source of truth in the dev repo. Push to `main` assumes an IAM role via OIDC (no static credentials) and publishes to S3; production EC2 hot-reloads on demand.
- **AWS Secrets Manager lifecycle** — secrets pulled at container startup; `.env` never committed. Compose overlay layering enforces env-appropriate values with startup guardrails.
- **Airflow cost tracking** — every OpenAI/Claude/DeepSeek call logs provider, operation, token counts, and USD cost to `llm_cost_tracking` in PostgreSQL. Cost visibility per DAG run.
- **Google Workspace super admin** — domain verification, mail routing, service account delegation, OAuth consent screen configuration.

---

## Stack

`Go` `Python` `TypeScript` `HCL / Terraform` `AWS` `EKS` `ArgoCD` `Datadog` `Kafka` `GitHub Actions`

---

[brianlopez.us](https://www.brianlopez.us) · Chicago, IL
