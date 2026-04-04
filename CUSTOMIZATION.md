# Customization Guide: Adapting This Framework for Your Organization

This repository is a **structural template** — a complete planning and configuration framework for building a multi-role AI engineering agent. It includes 9 role definitions, a domain extension system, infrastructure templates, and organizational guardrails. Any team — small or large — can fork, extend, and customize it.

The relevancy engineering domain is the reference implementation, but the framework is domain-agnostic. The roles (Architect, Developer, Tester, UX Expert, Product Manager, Project Manager, Program Manager, Data Scientist, Customer Persona) apply to any engineering team.

---

## How to Adopt This Framework

### Step 1: Fork the Repository

```bash
# Fork on GitHub, then clone
git clone https://github.com/YOUR_ORG/YOUR_FORK.git
cd YOUR_FORK
```

### Step 2: Fill Out the Organization Profile

Create `org/profile.md` to define your organization's specific context:

```markdown
# Organization Profile

## Team
- Team name: [your team name]
- Domain: [relevancy engineering / ML platform / data engineering / etc.]
- Team size: [number]
- Key roles: [list roles and what they do]

## Mission
[What does this team exist to do?]

## Customers
[Who uses what this team builds? Internal? External? Both?]
```

### Step 3: Fill Out the Infrastructure Decision Record

Copy and complete the template from `plan/05-foundational-tools.md`:

```bash
cp plan/05-foundational-tools.md org/infrastructure.md
# Edit org/infrastructure.md — fill in every "YOUR_ORG" section
```

### Step 4: Configure Roles

The 9 roles in `roles/` are designed to be universal. Customize by:

- **Keeping all 9** if your team needs the full spectrum
- **Prioritizing a subset** (e.g., small teams might focus on Developer + Tester + PjM)
- **Adding new roles** by creating `roles/<name>.md` following the existing template
- **Adjusting role perspectives** to match your team's culture and decision-making style

### Step 5: Add Your Domain

Create your domain knowledge in `domains/<your-domain>/`:

```bash
mkdir -p domains/your-domain
# Copy structure from domains/relevancy/ as template
cp domains/relevancy/overview.md domains/your-domain/
cp domains/relevancy/skills.md domains/your-domain/
cp domains/relevancy/evaluation.md domains/your-domain/
cp domains/relevancy/workflows.md domains/your-domain/
cp domains/relevancy/glossary.md domains/your-domain/
# Edit each file to replace relevancy content with your domain
```

The plan documents (`plan/`) are mostly domain-agnostic now. You only need to customize:

| File | What to Customize |
|------|------------------|
| `domains/<name>/*.md` | Your domain knowledge (primary customization) |
| `plan/phases/*.md` | Adjust phase timing to your needs |
| `tools/` | Keep tools you use, remove others, add new ones |
| `templates/` | Replace with your documentation templates |

### Step 6: Add Your Policies and Guardrails

Edit `org/policies.md` (see Guardrails section below).

### Step 7: Configure the Agent

Create your CLAUDE.md (or equivalent for your AI tool) using the context from your org profile, role selections, domain knowledge, and infrastructure decisions.

---

## Extension Points

Every section of this framework has clearly marked extension points. Look for:

```markdown
### Organization Extension Point
> **YOUR_ORG:** [description of what to fill in]
```

These appear throughout:

| Document | Extension Points |
|----------|-----------------|
| `plan/05-foundational-tools.md` | Infrastructure choices at every layer |
| `plan/04-foundational-skills.md` | Domain-specific skill requirements |
| `plan/02-architecture.md` | Technology stack choices |
| `plan/01-capabilities.md` | Domain-specific capabilities |
| `plan/phases/*.md` | Phase timing and deliverables |

---

## Adding Your Domain

### Domain Skill Template

When replacing relevancy engineering skills with your domain, follow this structure:

```markdown
# Foundational Skills for [Your Domain] Engineering Agent

## The End-to-End Problem-Solving Journey

### Stage 1: Problem Understanding
[How problems in your domain are reported and understood]
- What signals indicate a problem?
- What questions must be asked to scope the problem?
- What data helps classify the problem type?

### Stage 2: Problem Diagnosis
[How problems in your domain are diagnosed]
- What system components could be responsible?
- What diagnostic tools and techniques exist?
- What data must be collected?

### Stage 3: Root Cause Analysis
[How to find the root cause in your domain]
- What are the common root cause categories?
- What technical knowledge is needed?
- What differentiates symptoms from causes?

### Stage 4: Solution Design
[How solutions are designed in your domain]
- What are the common solution patterns?
- What tradeoffs must be considered?
- What constraints exist?

### Stage 5: Implementation
[How solutions are built in your domain]
- What technologies are used?
- What coding patterns are standard?
- What testing is required?

### Stage 6: Evaluation
[How changes are validated in your domain]
- What metrics prove the fix works?
- What regression checks are needed?
- What defines "good enough"?

### Stage 7: Impact Measurement
[How business impact is quantified in your domain]
- What business metrics are affected?
- How is causation established?
- How is impact reported to stakeholders?

### Stage 8: Documentation
[How work is documented in your domain]
- What must be documented?
- Where does documentation live?
- What format do stakeholders expect?
```

### Example Domains

This framework can be adapted for:

| Domain | Key Differences from Relevancy |
|--------|-------------------------------|
| **ML Platform Engineering** | Replace eval metrics with model metrics (accuracy, F1). Replace search pipeline with ML pipeline (training, serving, monitoring). |
| **Data Engineering** | Replace ranking with data quality. Replace search queries with data pipelines. Replace NDCG with data freshness, completeness, accuracy. |
| **Backend Engineering** | Replace eval with load/perf testing. Replace ranking with API design. Replace search metrics with SLA metrics (latency, availability). |
| **Frontend Engineering** | Replace eval with visual regression tests. Replace ranking with UX metrics. Replace search pipeline with component architecture. |
| **Security Engineering** | Replace eval with security scanning. Replace ranking with risk scoring. Replace search metrics with vulnerability metrics (CVSS, time-to-remediate). |
| **SRE/Platform** | Replace eval with reliability testing. Replace ranking with incident management. Replace search metrics with SLI/SLO. |
| **DevOps** | Replace eval with deployment validation. Replace ranking with pipeline optimization. Replace search metrics with DORA metrics. |

---

## Policies, Standards, and Guardrails

### Creating Your Policy File

Create `org/policies.md` to define boundaries for the AI agent:

```markdown
# Agent Policies and Guardrails

## Data Policies

### What the Agent CAN Access
- [ ] Source code in approved repositories
- [ ] Non-production databases (staging, dev)
- [ ] Public documentation and knowledge bases
- [ ] Anonymized/aggregated analytics data
- [ ] CI/CD logs and build artifacts

### What the Agent CANNOT Access
- [ ] Production databases (read or write)
- [ ] Customer PII (personally identifiable information)
- [ ] Authentication secrets and credentials
- [ ] Financial data or payment information
- [ ] Other teams' private repositories without permission

### What the Agent CANNOT Send to External AI APIs
- [ ] Customer data (even anonymized)
- [ ] Authentication tokens or secrets
- [ ] Internal architecture diagrams
- [ ] Unreleased product information
- [ ] HR or legal documents

## Code Policies

### What the Agent CAN Do
- [ ] Create feature branches
- [ ] Commit to feature branches
- [ ] Create pull requests
- [ ] Run tests and evaluations
- [ ] Update documentation

### What the Agent CANNOT Do
- [ ] Merge pull requests without human review
- [ ] Push directly to main/master/release branches
- [ ] Modify CI/CD pipeline configurations without review
- [ ] Delete branches, tags, or repositories
- [ ] Disable tests, linting, or security checks
- [ ] Add new external dependencies without review

## Workflow Policies

### What the Agent CAN Do
- [ ] Update Jira story status
- [ ] Add comments to Jira stories
- [ ] Create Confluence pages in designated spaces
- [ ] Post updates to designated Slack channels

### What the Agent CANNOT Do
- [ ] Close Jira stories (only move to "In Review")
- [ ] Modify other teams' Jira stories
- [ ] Delete Confluence pages
- [ ] Send direct messages to individuals without being asked
- [ ] Create or modify alerts/on-call schedules

## Quality Guardrails

### Before Any Code Change
- [ ] Tests must pass
- [ ] Linting must pass
- [ ] No security vulnerabilities introduced (Snyk/Trivy clean)
- [ ] Code coverage does not decrease

### Before Any Ranking Change
- [ ] Evaluation suite must run
- [ ] No metric regression beyond threshold (configurable)
- [ ] Regressions must be documented with justification
- [ ] Change must be linked to a Jira story

### Before Any Documentation
- [ ] Content reviewed for accuracy (no hallucinated facts)
- [ ] Cross-references verified (links work)
- [ ] Follows organization's documentation style guide
- [ ] Published to correct Confluence space/hierarchy

## Escalation Policies

### When the Agent Must Escalate to a Human
- [ ] Confidence below threshold on a task
- [ ] Evaluation shows regression without clear explanation
- [ ] Task requires access the agent doesn't have
- [ ] Task involves production changes
- [ ] Task affects multiple teams or services
- [ ] Task involves customer-facing changes
- [ ] Estimated scope exceeds [X hours] of agent time
- [ ] Agent encounters conflicting requirements
```

### Enforcement Mechanisms

Policies are only as good as their enforcement. Implement guardrails through:

| Mechanism | Where | What It Enforces |
|-----------|-------|------------------|
| **Branch protection** | Git platform | No direct push to main, required reviews |
| **CI gates** | CI pipeline | Tests, lint, security scan must pass |
| **MCP server permissions** | Agent config | Agent can only call allowed operations |
| **API tokens with limited scope** | Integration config | Agent's Jira/Confluence access is scoped |
| **Claude Code hooks** | Agent config | Pre/post action validation |
| **CLAUDE.md instructions** | Project config | Behavioral guidelines for the AI |
| **Evaluation gates** | CI pipeline | Ranking changes must pass eval threshold |
| **Audit logging** | All integrations | Every agent action is logged |

---

## Scaling Across Teams

### Single Team (Starting Point)

```
engineering-agent/            # One repo per team
+-- org/                     # Team-specific configuration
+-- roles/                   # Shared role definitions (may customize)
+-- domains/<team-domain>/   # Team's domain knowledge
+-- plan/                    # Team's agent plan
+-- tools/                   # Team's tool guides
+-- agent-core/              # Team's agent implementation
```

### Multiple Teams (Shared Foundation)

```
engineering-agent-framework/  # Shared repo: roles, tools, plan
+-- roles/                   # 9 role definitions (shared)
+-- plan/                    # Generic plans and skills
+-- tools/                   # Tool guides (shared)
+-- templates/               # Shared templates

team-relevancy/              # Team fork (inherits framework)
+-- org/                     # Relevancy team config
+-- domains/relevancy/       # Relevancy domain knowledge
+-- agent-core/              # Relevancy agent implementation

team-ml-platform/            # Another team fork
+-- org/                     # ML platform team config
+-- domains/ml-platform/     # ML domain knowledge
+-- agent-core/              # ML agent implementation
```

### Organization-Wide (Central Governance)

```
engineering-agent-platform/   # Central platform team manages
+-- framework/               # Shared framework (this repo)
+-- governance/              # Organization-wide policies
|   +-- data-policies.md
|   +-- security-standards.md
|   +-- ai-usage-guidelines.md
|   +-- approved-tools.md
+-- teams/                   # Per-team configurations
    +-- relevancy/
    +-- ml-platform/
    +-- backend/
    +-- frontend/
```

---

## Configuration as Code

Everything in this framework is version-controlled and code-reviewable:

| Configuration | Location | Format | Reviewable? |
|--------------|----------|--------|-------------|
| Agent behavior | `CLAUDE.md` | Markdown | Yes (PR review) |
| Role definitions | `roles/*.md` | Markdown | Yes |
| Domain knowledge | `domains/<name>/*.md` | Markdown | Yes |
| Tool access | `settings.json` / MCP config | JSON | Yes |
| Policies | `org/policies.md` | Markdown | Yes |
| Infrastructure | `org/infrastructure.md` | Markdown | Yes |
| CI/CD gates | `.github/workflows/` | YAML | Yes |
| Templates | `templates/` | Jinja2/Markdown | Yes |
| Evaluation thresholds | `config/eval-thresholds.yaml` | YAML | Yes |

Changes to any of these go through the same PR review process as code changes. The agent's behavior is governed by reviewable, auditable configuration — not hidden settings.

---

## Getting Started Checklist

For a new team adopting this framework:

- [ ] Fork this repository
- [ ] Fill out `org/profile.md` with team context
- [ ] Fill out `org/infrastructure.md` with tech stack decisions
- [ ] Fill out `org/policies.md` with guardrails
- [ ] Review `roles/` — keep all 9 or prioritize a subset for your team
- [ ] Create `domains/<your-domain>/` with domain knowledge (use `domains/relevancy/` as template)
- [ ] Set up approved AI tools from `tools/`
- [ ] Create CLAUDE.md referencing your roles, domain, and org config
- [ ] Configure MCP servers for your integrations
- [ ] Run Phase 1 to validate the agent works in your environment
- [ ] Iterate and extend — add roles, domains, integrations as needed
