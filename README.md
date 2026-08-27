# Ivan Triputen — Shipped Work

Senior DevOps / Platform Engineer. I run production infrastructure for game and product companies as a contractor: AWS/EKS, Terraform, CI/CD, observability, and AI-agent automation for ops.

- Site: [ivantriputen.pages.dev](https://ivantriputen.pages.dev/)
- Email: ivan.burusman@gmail.com

---

## Case 1 — Observability platform for a live web game

**Problem.** A production browser game ran on a legacy ELK stack: logs scattered across services, no tracing, and incident debugging meant SSH-ing into boxes. Finding the cause of a production issue took hours.

**What I did.**
- Migrated the logging pipeline from ELK to **Grafana Loki** with S3 object storage — one query language, no Elasticsearch cluster to babysit.
- Added distributed tracing on **Tempo** (S3-backed, with retention policies), instrumented the app once so the same setup works across all environments.
- Wired logs↔traces correlation in Grafana: click from an error log line straight to the request trace.
- Built alerting, uptime dashboards, and on-call runbooks on top.

**Result.** One pane of glass for logs, metrics, and traces. Root-cause analysis went from hours to minutes; log storage moved to cheap S3 instead of a managed Elasticsearch cluster.

---

## Case 2 — Zero-downtime EKS + CloudFront platform for a production web game

**Problem.** A web game with live traffic needed a proper cloud platform: reproducible infrastructure, automated deploys, and — the hard part — deploys that don't break sessions already open in players' browsers.

**What I did.**
- Built the platform on **AWS EKS + CloudFront**, fully described in **Terraform**, with GitLab CI/CD pipelines for build and deploy.
- Designed a three-layer client caching model: immutable hashed assets, no-cache entry points, and a localStorage layer — so a deploy rolls out safely under open tabs instead of serving players a half-updated bundle.
- Automated TLS certificate management and CDN invalidation as part of the pipeline.

**Result.** Deploys during live traffic with zero downtime and no broken client sessions; infrastructure reproducible from code; new environments spun up from the same modules.

---

## Case 3 — Multi-cloud CDN migration under production traffic

**Problem.** A product had to move its CDN between providers (compliance + cost) without user-visible breakage. After the initial switch, users hit intermittent navigation failures.

**What I did.**
- Planned and executed the CDN cutover for static assets and media under production traffic.
- Tracked down a subtle post-migration bug: the new CDN returned **conditional CORS headers** (present only when the request carried an `Origin` header), which broke Next.js client-side navigation for cached responses. Fixed the edge configuration to return CORS headers unconditionally.

**Result.** Migration completed with no downtime; the class of "works on refresh, breaks on navigation" errors eliminated.

---

## Case 4 — AI-agent automation for infrastructure operations

**Problem.** Routine ops — log triage, environment checks, release verification, monitoring sweeps — ate senior-engineer hours every week.

**What I did.**
- Built agentic pipelines on top of **Claude**: multi-agent workflows with structured outputs, verification gates, and human-in-the-loop approval for irreversible steps.
- Agents handle the investigation (querying live systems, correlating logs and configs); a human reviews and approves anything that changes state. Every run leaves an audit trail.
- Applied the same pattern to incident triage and infrastructure audits.

**Result.** Hours of routine investigation per week moved off the senior engineer; humans only touch decisions, not digging. This is the exact architecture I'd bring to teams building agentic products: retries, tool boundaries, observability, and human override are design inputs, not afterthoughts.

---

## Stack

AWS (EKS, CloudFront, S3, IAM) · Kubernetes · Terraform · GitLab CI/CD · Grafana / Loki / Tempo / Prometheus · Docker · Python / Bash · Claude agent pipelines

## Working with me

I take on fixed-scope contracts and monthly retainers (observability under-the-key, platform build-outs, cloud cost audits). I invoice through my account in Kazakhstan — standard international wire, no payment friction.
