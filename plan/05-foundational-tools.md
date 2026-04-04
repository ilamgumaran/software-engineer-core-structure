# Foundational Tools and Infrastructure

The previous document (`04-foundational-skills.md`) covers what the agent must **know**. This document covers what the agent must **use** — the full toolchain from source code to production, including the spectrum of deployment strategies from bare-metal to fully managed cloud.

Organizations adopting this framework will have different infrastructure. This document maps the complete toolchain landscape so teams can plug in their specific choices at each layer.

---

## The Full Toolchain Stack

```
Layer 7: AI/Agent Tools          Claude Code, Copilot, Gemini, Glean
Layer 6: Workflow & Project      Jira, Linear, Confluence, Notion
Layer 5: Observability           Logging, metrics, tracing, alerting
Layer 4: CI/CD & Testing         Build, test, deploy pipelines
Layer 3: Runtime & Orchestration Containers, K8s, serverless, bare-metal
Layer 2: Development Environment Local dev, cloud dev, devcontainers
Layer 1: Source Control          Git, branching strategy, code review
Layer 0: Operating System        Linux, macOS, Windows, RTOS
```

Each layer has multiple valid choices. The agent must understand the layer's purpose and adapt to whichever specific tools are in use.

---

## Layer 0: Operating System and Hardware

### Why This Matters

The choice between containerized, virtualized, or bare-metal deployment fundamentally affects how code is written, tested, and deployed. An agent that only knows Docker is useless to a team deploying to embedded systems.

### Options Spectrum

#### Bare-Metal / Direct-to-Hardware

**When to use:** Maximum performance, real-time requirements, embedded systems, GPU workloads, cost optimization at scale.

```
Application Code
    |
    v
System Libraries (libc, CUDA, etc.)
    |
    v
Operating System (Linux, RTOS, FreeBSD)
    |
    v
Hardware (CPU, GPU, FPGA, custom silicon)
```

**Agent skills needed:**
- Compile and link against system libraries directly
- Understand hardware-specific optimizations (SIMD, cache alignment, NUMA)
- Write code that manages its own memory efficiently
- Handle process management without container abstractions
- Configure systemd/supervisord for service management
- Understand kernel tuning for search workloads (vm.swappiness, file descriptors, TCP buffers)

**Relevancy engineering use case:** High-throughput search engines that need microsecond latency. Vector similarity search on GPU clusters. Custom inference servers for neural reranking.

**Prompt-to-code advantage:** AI agents can generate highly optimized, hardware-aware code that compiles to efficient binaries without the overhead of interpreted languages and container layers. For latency-critical ranking code:
```
Prompt: "Write a SIMD-optimized dot product for float32 vectors 
  of dimension 768, targeting AVX-512. No dependencies."
  
Output: C/C++/Rust code that compiles to a single binary, 
  no container, no runtime, no garbage collector.
```

#### Virtual Machines

**When to use:** Strong isolation, legacy systems, compliance requirements, multi-tenant environments.

```
Application Code
    |
    v
Guest OS (full OS per VM)
    |
    v
Hypervisor (KVM, VMware, Hyper-V)
    |
    v
Host Hardware
```

**Agent skills needed:**
- VM provisioning (Terraform, Vagrant, cloud VM APIs)
- OS-level configuration management (Ansible, Chef, Puppet)
- Network configuration within virtualized environments
- Snapshot and backup management

#### Containers

**When to use:** Portable deployments, microservice architectures, development-production parity, team standardization.

```
Application Code
    |
    v
Container Runtime (Docker, containerd, Podman)
    |
    v
Container Orchestration (Kubernetes, Docker Compose, ECS, Nomad)
    |
    v
Host OS / Cloud Infrastructure
```

**Agent skills needed:**
- Write Dockerfiles that produce small, secure images
- Multi-stage builds to separate build-time from runtime dependencies
- Docker Compose for local development environments
- Kubernetes manifests (Deployments, Services, ConfigMaps, Secrets)
- Helm charts for parameterized deployments
- Container security (non-root users, read-only filesystems, resource limits)

#### Serverless / Managed Services

**When to use:** Low operational overhead, event-driven workloads, variable traffic, rapid prototyping.

```
Application Code (function/handler)
    |
    v
Serverless Platform (Lambda, Cloud Functions, Cloud Run)
    |
    v
Cloud Provider Infrastructure
```

**Agent skills needed:**
- Write stateless, idempotent functions
- Understand cold start implications
- Configure API gateways and event triggers
- Manage state externally (databases, caches, queues)

### Decision Matrix

| Factor | Bare-Metal | VM | Container | Serverless |
|--------|-----------|-----|-----------|-----------|
| Performance | Best | Good | Good | Variable (cold starts) |
| Isolation | Process-level | Strong (hardware) | Moderate (namespace) | Strong (platform) |
| Portability | Low | Medium | High | Medium (vendor-specific) |
| Operational cost | High (you manage) | Medium | Medium | Low (provider manages) |
| Startup time | N/A (always running) | Minutes | Seconds | Milliseconds-seconds |
| Cost efficiency | Best at scale | Medium | Good | Best at low/variable load |
| Agent complexity | Highest | Medium | Medium | Lowest |

### Organization Extension Point

> **YOUR_ORG:** Document your deployment targets here. Which layers does your team deploy to? What are your constraints (compliance, latency, cost)?

---

## Layer 1: Source Control

### Git (Universal Foundation)

Git is the non-negotiable foundation. Every organization uses it. The agent must be fluent.

#### Core Git Skills

| Skill | Why It Matters | Agent Usage |
|-------|---------------|-------------|
| Branching and merging | Parallel work without conflicts | Feature branches per Jira story |
| Rebasing | Clean history for review | Rebase before PR creation |
| Cherry-picking | Selective change porting | Hotfix from feature branch to main |
| Bisecting | Find which commit introduced a bug | Automated regression hunting |
| Stashing | Context switching without losing work | Pause mid-task for urgent work |
| Submodules/subtrees | Multi-repo dependencies | Shared evaluation libraries |
| Hooks | Automated checks on commit/push | Pre-commit linting, post-commit Jira updates |
| Worktrees | Multiple branches checked out simultaneously | Run evaluation on two configs in parallel |

#### Branching Strategies

The agent must adapt to the organization's branching model:

| Strategy | Description | Best For |
|----------|-------------|----------|
| **GitHub Flow** | main + short-lived feature branches | Small teams, continuous deployment |
| **GitFlow** | main + develop + feature + release + hotfix | Scheduled releases, multiple environments |
| **Trunk-Based** | main + very short branches (< 1 day) | CI/CD mature teams, feature flags |
| **Release Branching** | main + long-lived release branches | Multiple product versions in production |

**Agent behavior adapts to strategy:**
```
# GitHub Flow (default)
agent task --jira REL-456
→ Creates: feat/REL-456-description (from main)
→ PR target: main

# GitFlow
agent task --jira REL-456
→ Creates: feature/REL-456-description (from develop)
→ PR target: develop

# Trunk-Based
agent task --jira REL-456
→ Creates: REL-456 (from main, short-lived)
→ PR target: main (with feature flag if incomplete)
```

#### Git Hosting Platforms

| Platform | Strengths | API/CLI |
|----------|-----------|---------|
| **GitHub** | Largest ecosystem, Actions CI, Copilot integration | `gh` CLI, REST + GraphQL API |
| **GitLab** | Built-in CI/CD, self-hosted option, DevSecOps | `glab` CLI, REST + GraphQL API |
| **Bitbucket** | Atlassian integration (Jira/Confluence native) | REST API, Pipes CI |
| **Azure DevOps** | Microsoft ecosystem, enterprise features | `az repos` CLI, REST API |
| **Gitea/Forgejo** | Self-hosted, lightweight, open source | REST API |

**Agent must support:** Whichever platform the organization uses. The git operations are the same; the API layer (PRs, reviews, CI status) differs.

#### Code Review

The agent participates in code review in two ways:

1. **As author:** Creates PRs with clear descriptions, responds to review comments, makes requested changes
2. **As reviewer:** Analyzes diffs for correctness, convention adherence, test coverage, and relevancy impact

**Review checklist the agent applies:**
- [ ] Changes match the Jira story requirements
- [ ] Tests cover the new/changed code
- [ ] No relevancy regressions introduced (run eval if ranking-related)
- [ ] Follows repository coding conventions
- [ ] No secrets or credentials committed
- [ ] Documentation updated if user-facing behavior changed
- [ ] Performance impact considered (latency-sensitive paths)

### Organization Extension Point

> **YOUR_ORG:** Document your git hosting platform, branching strategy, branch protection rules, required reviewers, and merge requirements (squash? rebase? merge commit?).

---

## Layer 2: Development Environment

### Local Development

The agent must work within the team's local development setup.

#### Option A: Native Development

```
Developer Machine (macOS/Linux/Windows)
    |
    +-- Language runtimes (Python 3.11, Node 20, Java 21, Rust, Go)
    +-- Package managers (pip, npm, maven, cargo)
    +-- Database servers (PostgreSQL, Redis, Elasticsearch)
    +-- Tools (make, just, task)
```

**Agent skills:**
- Detect installed runtimes and versions
- Manage virtual environments (venv, conda, nvm, sdkman)
- Handle platform differences (macOS vs. Linux paths, libraries)
- Install and configure local services

#### Option B: Dev Containers

Standardized development environments using containers.

```json
// .devcontainer/devcontainer.json
{
  "name": "Relevancy Engineering",
  "image": "mcr.microsoft.com/devcontainers/python:3.11",
  "features": {
    "ghcr.io/devcontainers/features/node:1": {},
    "ghcr.io/devcontainers/features/docker-in-docker:2": {}
  },
  "postCreateCommand": "pip install -e '.[dev]'",
  "customizations": {
    "vscode": {
      "extensions": [
        "github.copilot",
        "ms-python.python",
        "ms-python.vscode-pylance"
      ]
    }
  }
}
```

**Agent skills:**
- Read and modify devcontainer configuration
- Build and troubleshoot container environments
- Understand volume mounts and port forwarding
- Handle devcontainer lifecycle (create, rebuild, connect)

#### Option C: Cloud Development Environments

Remote development in cloud-hosted environments.

| Platform | Description |
|----------|-------------|
| **GitHub Codespaces** | Cloud dev environments from any repo |
| **Gitpod** | Automated, pre-built cloud workspaces |
| **AWS Cloud9** | Browser-based IDE with AWS integration |
| **Google Cloud Shell** | Browser-based terminal with GCP tools |
| **Coder** | Self-hosted remote development platform |

**Agent skills:**
- Provision and configure cloud dev environments
- Handle network constraints (SSH tunneling, port forwarding)
- Manage persistent storage and state
- Optimize for latency (choosing region, instance type)

#### Option D: AI-Optimized Development (Prompt-to-Code-to-Binary)

For performance-critical components, the agent can generate code that compiles directly to optimized binaries without runtime overhead.

**Workflow:**
```
Requirement: "Score 10M documents per second with 768-dim embeddings"
    |
    v
Agent generates: Rust/C++ code with SIMD intrinsics
    |
    v
Compiles to: Native binary (no container, no runtime, no GC)
    |
    v
Deploys to: Bare-metal or VM with direct hardware access
    |
    v
Performance: 10x+ vs interpreted language in container
```

**When to use this approach:**
- Inner loops of ranking/scoring functions
- Vector similarity computation
- Real-time feature extraction
- High-throughput data processing
- Edge/embedded deployments

**Agent skills for prompt-to-compiled-code:**
- Generate correct C, C++, Rust, or Go code from requirements
- Write proper build systems (CMake, Cargo, Makefile)
- Apply compiler optimizations (-O3, LTO, PGO)
- Profile and benchmark generated code
- Handle cross-compilation for target architectures
- Integrate compiled components with higher-level orchestration

### Build Systems

| Tool | Language | Description |
|------|----------|-------------|
| **Make** | Any | Universal, ubiquitous, simple |
| **Just** | Any | Modern Make alternative, better syntax |
| **Task** | Any | YAML-based task runner |
| **CMake** | C/C++ | Cross-platform build system |
| **Cargo** | Rust | Build + package manager |
| **Bazel** | Any | Hermetic builds, massive monorepo support |
| **Gradle** | JVM | Flexible, plugin-rich |
| **Poetry/PDM** | Python | Modern Python project management |
| **Turborepo/Nx** | JS/TS | Monorepo build orchestration |

### Organization Extension Point

> **YOUR_ORG:** Document your standard development environment setup. Include: required tools, IDE configuration, local service dependencies, and any setup scripts.

---

## Layer 3: Runtime and Orchestration

### Container Orchestration

#### Docker (Foundation)

Every containerized deployment starts with Docker knowledge.

**Agent must produce:**
```dockerfile
# Multi-stage build for Python search service
FROM python:3.11-slim AS builder
WORKDIR /app
COPY pyproject.toml .
RUN pip install --no-cache-dir .

FROM python:3.11-slim AS runtime
COPY --from=builder /usr/local/lib/python3.11/site-packages /usr/local/lib/python3.11/site-packages
COPY src/ /app/src/
USER nobody
EXPOSE 8080
CMD ["python", "-m", "uvicorn", "app:main", "--host", "0.0.0.0", "--port", "8080"]
```

**Skills:** Image optimization, layer caching, security scanning, registry management.

#### Kubernetes

For production-grade container orchestration.

**Agent must understand:**
- Pods, Deployments, StatefulSets, DaemonSets
- Services, Ingress, NetworkPolicies
- ConfigMaps, Secrets (and external secret management)
- Resource requests/limits, HPA (Horizontal Pod Autoscaler)
- Helm charts for parameterized deployments
- Operators for complex stateful applications (Elasticsearch Operator, etc.)

#### Alternatives to Kubernetes

| Platform | When to Use |
|----------|------------|
| **Docker Compose** | Local dev, small deployments |
| **Docker Swarm** | Simple orchestration without K8s complexity |
| **Nomad** | HashiCorp ecosystem, simpler than K8s |
| **ECS/Fargate** | AWS-native, serverless containers |
| **Cloud Run** | Stateless containers, auto-scaling to zero |
| **Fly.io** | Edge deployment, simple scaling |

### Bare-Metal Service Management

For direct-to-hardware deployments without container overhead.

**Agent must know:**
| Tool | Purpose |
|------|---------|
| **systemd** | Service lifecycle management on Linux |
| **supervisord** | Process management (cross-platform) |
| **Ansible** | Configuration management and deployment |
| **Terraform** | Infrastructure provisioning |
| **Packer** | Machine image creation |

**Deployment workflow for bare-metal:**
```
Code → Compile → Package (deb/rpm/tar) → Deploy to hosts → Restart service
                                            |
                                            +-- Ansible playbook
                                            +-- or rsync + systemctl
                                            +-- or custom deploy script
```

### Organization Extension Point

> **YOUR_ORG:** Document your runtime environment. Include: container platform (if any), orchestration tool, deployment targets, and service mesh configuration.

---

## Layer 4: CI/CD and Testing

### Continuous Integration

The agent must work with the team's CI system to validate changes automatically.

#### CI Platforms

| Platform | Strengths | Config Format |
|----------|-----------|--------------|
| **GitHub Actions** | GitHub-native, huge marketplace | YAML (`.github/workflows/`) |
| **GitLab CI** | GitLab-native, powerful pipelines | YAML (`.gitlab-ci.yml`) |
| **Jenkins** | Self-hosted, maximum flexibility | Groovy (`Jenkinsfile`) |
| **CircleCI** | Fast, good caching, orbs ecosystem | YAML (`.circleci/config.yml`) |
| **Buildkite** | Self-hosted agents, cloud dashboard | YAML (`.buildkite/pipeline.yml`) |
| **Tekton** | Kubernetes-native CI/CD | YAML (K8s CRDs) |
| **Dagger** | Programmable CI (Go/Python/TS) | Code |
| **Earthly** | Containerized builds, reproducible | Earthfile |

**Agent CI skills:**
- Write and modify CI pipeline configurations
- Debug failed builds from CI logs
- Optimize pipeline speed (caching, parallelism, selective testing)
- Manage CI secrets and environment variables
- Set up branch protection and required checks

#### CI Pipeline for Relevancy Engineering

```yaml
# Example: GitHub Actions pipeline
name: Relevancy Agent CI
on: [push, pull_request]

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: pip install ruff black
      - run: ruff check . && black --check .

  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: pip install -e ".[dev]"
      - run: pytest --cov=src --cov-report=xml

  eval-smoke:
    runs-on: ubuntu-latest
    if: contains(github.event.pull_request.labels.*.name, 'ranking-change')
    steps:
      - uses: actions/checkout@v4
      - run: pip install -e .
      - run: agent eval --config configs/smoke.yaml --compare baseline
      - run: |
          # Fail if NDCG dropped more than 2%
          python -c "
          import json
          results = json.load(open('eval-results.json'))
          assert results['ndcg_delta'] > -0.02, f'NDCG regression: {results[\"ndcg_delta\"]}'
          "
```

### Continuous Deployment

| Strategy | Description | Risk Level |
|----------|-------------|-----------|
| **Blue-Green** | Two identical environments, switch traffic | Low (instant rollback) |
| **Canary** | Gradual rollout to % of traffic | Low (early detection) |
| **Rolling** | Update instances one at a time | Medium |
| **Feature Flags** | Deploy code but gate behind flags | Low (decouple deploy from release) |
| **GitOps** | Git as source of truth for deployment state | Low (auditable, declarative) |

**Agent must know:**
- How to configure deployment strategies for the team's platform
- How to monitor canary deployments for regressions
- How to trigger rollbacks automatically on metric degradation
- How to manage feature flags for relevancy experiments

### Testing Infrastructure

#### Testing Pyramid for Search/Relevancy

```
                    /\
                   /  \
                  / E2E \          End-to-end search tests
                 /--------\        (full query -> results -> metrics)
                / Integration\     Component integration
               /--------------\    (parser + retriever + ranker)
              /     Unit       \   Individual functions
             /------------------\  (metric calc, config parser, scorer)
```

**Test categories the agent must handle:**

| Layer | Tool Options | What It Tests |
|-------|-------------|---------------|
| Unit | pytest, Jest, JUnit, cargo test | Individual functions in isolation |
| Integration | pytest + testcontainers, docker-compose | Components working together |
| E2E / Evaluation | Custom evaluation framework | Full search pipeline quality |
| Performance | Locust, k6, wrk, Gatling | Latency and throughput under load |
| Chaos | Chaos Monkey, Litmus, Toxiproxy | Resilience to failures |
| Security | Bandit, Snyk, Trivy, OWASP ZAP | Vulnerabilities and exposures |
| Data quality | Great Expectations, dbt tests, Soda | Data correctness and completeness |

**Evaluation as a CI gate:**
The relevancy evaluation suite is a special kind of test — it gates ranking changes the same way unit tests gate code changes. The agent must know how to:
- Run fast "smoke" evaluations in CI (subset of queries, <2 min)
- Run full evaluations as a scheduled or manual job
- Interpret evaluation results as pass/fail gates
- Report evaluation metrics on PRs

### Organization Extension Point

> **YOUR_ORG:** Document your CI/CD platform, pipeline structure, deployment strategy, test requirements for merge, and evaluation gates.

---

## Layer 5: Observability

### Why Observability Matters for Relevancy

Relevancy problems often surface in production — not in evaluation suites. The agent must monitor production signals to detect and diagnose issues.

### Three Pillars

#### Logging

| Tool | Type | Best For |
|------|------|----------|
| **ELK Stack** (Elasticsearch, Logstash, Kibana) | Self-hosted | Full control, large scale |
| **Loki + Grafana** | Self-hosted/cloud | Cost-effective, K8s-native |
| **Datadog Logs** | SaaS | All-in-one platform |
| **CloudWatch / Cloud Logging** | Cloud-native | AWS/GCP integration |
| **Splunk** | Enterprise | Compliance, enterprise features |

**Relevancy-specific logs the agent should analyze:**
- Search request/response logs (query, results, latency)
- Click and engagement event logs
- Ranking score debug logs (explain output)
- Feature computation logs
- A/B test assignment logs

#### Metrics

| Tool | Type | Best For |
|------|------|----------|
| **Prometheus + Grafana** | Self-hosted | K8s-native, pull-based |
| **Datadog** | SaaS | All-in-one, easy setup |
| **New Relic** | SaaS | APM-focused |
| **CloudWatch / Cloud Monitoring** | Cloud-native | Cloud integration |
| **InfluxDB + Telegraf** | Self-hosted | Time-series focused |

**Relevancy-specific metrics:**
- Search latency (p50, p95, p99)
- Query volume and error rate
- Click-through rate (real-time)
- Zero-result rate
- Cache hit rate
- Ranking model inference latency
- Feature computation latency

#### Tracing

| Tool | Type | Best For |
|------|------|----------|
| **Jaeger** | Self-hosted | OpenTelemetry native |
| **Zipkin** | Self-hosted | Simple, lightweight |
| **Datadog APM** | SaaS | Full-stack tracing |
| **AWS X-Ray** | Cloud-native | AWS services |
| **Honeycomb** | SaaS | High-cardinality exploration |

**Relevancy-specific traces:**
- Full search request lifecycle (query parse -> retrieve -> rank -> present)
- Per-stage latency breakdown
- Feature computation timelines
- External service calls (embedding API, ML model server)

### Alerting

The agent should understand alerting patterns for relevancy:
| Signal | Alert Condition | Severity |
|--------|----------------|----------|
| CTR drop | >10% decrease over 1 hour vs. same hour last week | P1 |
| Zero-result spike | >5% of queries returning zero results | P1 |
| Latency spike | p95 > 500ms for >5 minutes | P2 |
| Evaluation regression | NDCG drops >2% in scheduled eval | P2 |
| Index staleness | Index not updated in >2x expected interval | P3 |

### Organization Extension Point

> **YOUR_ORG:** Document your observability stack, key dashboards, alerting channels, and on-call procedures for search/relevancy incidents.

---

## Layer 6: Workflow and Project Management

### Issue Tracking

| Tool | Strengths | Best For |
|------|-----------|---------|
| **Jira** | Enterprise standard, deep customization | Large orgs, complex workflows |
| **Linear** | Fast, opinionated, developer-focused | Startups, engineering teams |
| **GitHub Issues** | Integrated with code, free | Small teams, OSS |
| **GitLab Issues** | Integrated with CI/CD | GitLab shops |
| **Azure Boards** | Microsoft ecosystem | Azure DevOps users |
| **Shortcut** | Balance of power and simplicity | Mid-size teams |
| **Plane** | Open-source Jira alternative | Self-hosted preference |

### Documentation

| Tool | Strengths | Best For |
|------|-----------|---------|
| **Confluence** | Enterprise standard, Jira integration | Large orgs |
| **Notion** | Flexible, good UX, databases | Startups, cross-functional teams |
| **GitBook** | Developer docs, Git-backed | Technical documentation |
| **Docusaurus** | Static site, versioned docs | Open-source projects |
| **Markdown in repo** | Co-located with code, versioned | Engineer-focused teams |
| **Outline** | Open-source Notion alternative | Self-hosted preference |
| **Slite** | Simple, team-focused | Small teams |

### Communication

| Tool | Agent Integration |
|------|------------------|
| **Slack** | Webhook notifications, slash commands, bot messages |
| **Microsoft Teams** | Webhook notifications, bot framework |
| **Discord** | Webhook notifications, bot API |
| **Email** | SMTP for reports and summaries |

### Organization Extension Point

> **YOUR_ORG:** Document your project management tools, documentation platform, communication channels, and how the agent should interact with each.

---

## Layer 7: AI/Agent Tools

Covered in detail in `tools/` directory. Summary of the landscape:

### Code Generation and Execution

| Tool | Modality | Strengths |
|------|----------|-----------|
| **Claude Code** | CLI agent | Full tool access, autonomous execution |
| **GitHub Copilot** | IDE extension | Real-time completions, chat |
| **Cursor** | AI-native IDE | Deep codebase awareness |
| **Windsurf** | AI-native IDE | Agent-like coding assistance |
| **Aider** | CLI agent | Git-aware, multi-file editing |
| **Amazon Q Developer** | IDE + CLI | AWS integration |
| **Tabnine** | IDE extension | Privacy-focused, self-hosted option |

### Enterprise Knowledge

| Tool | Modality | Strengths |
|------|----------|-----------|
| **Glean** | Enterprise search | Cross-platform search, AI answers |
| **Gemini Enterprise** | Workspace AI | Google Workspace integration, large context |
| **Microsoft 365 Copilot** | Workspace AI | Office integration |
| **Perplexity Enterprise** | AI search | Web + internal search |

### Organization Extension Point

> **YOUR_ORG:** Document which AI tools are approved for use, any data governance restrictions, and API access policies.

---

## Infrastructure Decision Record Template

When an organization adopts this framework, they should fill out this decision record:

```markdown
# Infrastructure Decision Record: [ORG_NAME]

## Source Control
- Platform: [GitHub / GitLab / Bitbucket / Azure DevOps]
- Branching strategy: [GitHub Flow / GitFlow / Trunk-Based]
- Code review requirements: [# of approvals, required reviewers]

## Development Environment
- Standard setup: [Native / Dev Container / Cloud IDE]
- Required tools: [list]
- Setup automation: [script/tool name]

## Runtime
- Primary deployment target: [K8s / ECS / Bare-metal / Serverless]
- Container registry: [ECR / GCR / Docker Hub / self-hosted]
- Performance-critical components: [Container / Bare-metal / GPU]

## CI/CD
- CI platform: [GitHub Actions / GitLab CI / Jenkins / etc.]
- Deployment strategy: [Blue-Green / Canary / Rolling / GitOps]
- Required gates: [tests, linting, security scan, eval]

## Observability
- Logging: [ELK / Loki / Datadog / CloudWatch]
- Metrics: [Prometheus / Datadog / CloudWatch]
- Tracing: [Jaeger / Datadog / X-Ray]
- Alerting: [PagerDuty / OpsGenie / Slack]

## Workflow
- Issue tracking: [Jira / Linear / GitHub Issues]
- Documentation: [Confluence / Notion / Markdown]
- Communication: [Slack / Teams / Discord]

## AI Tools
- Approved tools: [list]
- Data governance: [restrictions on code/data sent to AI APIs]
- API access: [direct / proxy / self-hosted]

## Languages and Frameworks
- Primary languages: [Python, TypeScript, Rust, etc.]
- Search engine: [Elasticsearch / Solr / Vespa / custom]
- Data warehouse: [BigQuery / Snowflake / Redshift / Databricks]
```

---

## Portability Matrix

This framework is designed to be portable across environments. Here's how each component adapts:

| Component | Cloud-Native | On-Premise | Hybrid | Edge |
|-----------|-------------|-----------|--------|------|
| Source control | GitHub/GitLab SaaS | GitLab/Gitea self-hosted | Either | Git with remote sync |
| Dev environment | Codespaces/Gitpod | Dev containers on local | VPN + cloud IDE | Local native |
| Runtime | K8s on cloud | K8s on-prem or bare-metal | Multi-cluster K8s | Direct-to-hardware |
| CI/CD | GitHub Actions/Cloud Build | Jenkins/Buildkite agents | Split pipelines | Cross-compile + deploy |
| Observability | Datadog/CloudWatch | Prometheus/Grafana stack | Federated metrics | Local logging + remote push |
| AI tools | Cloud APIs | Self-hosted models (Ollama, vLLM) | Hybrid routing | On-device models |

### Fully Air-Gapped / On-Premise Stack

For organizations that cannot use cloud services:

```
Source Control:  Gitea or GitLab CE (self-hosted)
Dev Environment: Dev containers on local machines
Runtime:         K8s (kubeadm/k3s) or bare-metal with Ansible
CI/CD:           Jenkins or Buildkite with self-hosted agents
Observability:   Prometheus + Grafana + Loki + Jaeger (all self-hosted)
AI Tools:        Ollama/vLLM with open models (Llama, Mistral, CodeLlama)
Issue Tracking:  Plane or GitLab Issues
Documentation:   Outline or Markdown in repo
Search Engine:   Elasticsearch/OpenSearch (self-hosted)
Data Warehouse:  ClickHouse or PostgreSQL with TimescaleDB
```

The framework still works — the tools change, the layers and skills remain the same.
