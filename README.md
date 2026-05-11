# Hi, I'm Brian

Staff Platform Engineer at [Grindr](https://github.com/blo-grindr) (NYSE: GRND) and founding engineer at [Farewell John](https://farewelljohn.com). I build cloud infrastructure, identity systems, and the automation that removes manual work from the loop.

**Scale:** 15M monthly active users, 190 countries, 8 AWS accounts, 5+ EKS clusters, $1.4M/year in cloud cost eliminated.

---

## What I Do

**Infrastructure as code** - Every system I own is Terraform-managed, PR-reviewed, and deployed without manual steps. If it isn't declarative, it isn't done.

**Identity and access** - Multi-account IAM federation, IRSA per-service scoping, OIDC-based CI/CD with zero static credentials. I've migrated orgs from legacy SSO to federated identity end-to-end.

**Automation pipelines** - Event-driven backends that propagate state changes across systems automatically. When something changes in one place, everything downstream reacts without a human in the loop.

**Developer experience** - CLIs, MCP servers, and environments that make engineers faster. If a person does the same thing twice, it gets automated.

---

## Projects

### [perfgate](https://github.com/thebrianlopez/perfgate)
Statistical performance gating for CI. Define a benchmark, set a regression threshold, fail the build. Simple contract, serious signal.

### [closed-loop-telemetry](https://github.com/thebrianlopez/closed-loop-telemetry)
JSONL event bus for AI-augmented engineering. Non-deterministic systems need observability that accounts for probabilistic outputs, not just pass/fail.

### [org-identity-bootstrap](https://github.com/thebrianlopez/org-identity-bootstrap)
Terraform modules for GitHub + AWS + GCP identity federation from scratch. Zero static credentials from day one. Designed to be the first thing you run in a new org.

### [aws-iam-patterns](https://github.com/thebrianlopez/aws-iam-patterns)
Declarative Terraform patterns for least-privilege IAM: role trust policies, boundary conditions, cross-account trust setups, and the guardrails that catch mistakes before production.

### [mcp-aws-inspector](https://github.com/thebrianlopez/mcp-aws-inspector)
MCP server that surfaces AWS IAM and S3 introspection directly into AI coding assistants. Security context in the tool that is already open.

---

## Farewell John ([hersolutionsllc](https://github.com/hersolutionsllc))

The **PRD** identified a consumer problem: families navigating a death shouldn't have to call a dozen funeral homes to compare prices. The **FDD** answered it with a clean separation principle — ingest data continuously in the background, serve it instantly from a read-only API — so the product could scale without coupling the user experience to crawl latency. The **TDD** made it operational: PostGIS for spatial search, Airflow DAGs for multi-source ingestion, CloudFront edge functions for zero-downtime maintenance, and a one-command local production clone so nothing ships untested. I owned the full chain from product spec to running infrastructure at [farewelljohn.com](https://farewelljohn.com).

| System | What it does |
|--------|-------------|
| Read-only API + Airflow pipeline | Express/Node.js serves PostgreSQL reads only. All ingestion (Google Places, Playwright crawler, OpenAI/Claude PDF parser) runs in Airflow DAGs. Hard service boundary between read and write paths. |
| PostGIS spatial cache | Airflow populates zipcodes at 50-mile radius. API filters to any smaller radius from the same cache row using `ST_DWithin`. Zero redundant external API calls. |
| OrbStack VM | `make orbstack-up` boots a local production clone via cloud-init, GHCR image pull, and S3 secrets bootstrap. Engineers test against the real stack before every deploy. |
| CloudFront edge functions | KVS-backed CF Functions return 503 at the edge without touching EC2. `/demo/*` always available. Zero-downtime maintenance window. |
| GitHub Actions + IAM | OIDC-based role assumption for all CI/CD. No static credentials anywhere in the pipeline. nginx configs published to S3 on push; EC2 hot-reloads on demand. |
| Secrets Manager lifecycle | Secrets pulled at container startup via `make secrets-pull`. Compose overlay layering enforces correct values per environment with startup guardrails. |
| Cost tracking | Every OpenAI/Claude/DeepSeek call logs provider, operation, token counts, and USD cost to PostgreSQL. Full cost visibility per DAG run. |
| Google Workspace admin | Domain verification, mail routing, service account delegation, OAuth consent screen configuration. |

---

## Stack

`Go` `Python` `TypeScript` `HCL / Terraform` `AWS` `EKS` `ArgoCD` `Datadog` `PostgreSQL` `Airflow` `GitHub Actions`

---

[brianlopez.us](https://www.brianlopez.us) · Chicago, IL
