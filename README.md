# Multi-Role Software Engineering Agent Framework

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An open, forkable framework for building AI-powered engineering agents that operate across **9 roles** — Architect, Developer, Tester, UX Expert, Product Manager, Project Manager, Program Manager, Data Scientist, and Customer Persona. The agent switches roles based on the task, works within your existing workflow, and is configurable for any engineering domain.

**This repo is both the plan and the prompt.** Fork it, plug in your domain and infrastructure, and you have a complete agent configuration for your team.

---

## The 9 Roles

| Role | What It Does |
|------|-------------|
| **Architect** | Designs systems, evaluates tradeoffs, produces ADRs |
| **Developer** | Writes, modifies, and debugs code across the stack |
| **Tester** | Validates correctness, finds edge cases, ensures quality |
| **UX Expert** | Designs experiences, audits accessibility, advocates for users |
| **Product Manager** | Defines what to build and why, writes requirements |
| **Project Manager** | Plans sprints, tracks progress, manages risks |
| **Program Manager** | Coordinates across teams, manages dependencies |
| **Data Scientist** | Analyzes data, builds models, designs experiments |
| **Customer Persona** | Simulates customer reactions, validates UX from user perspectives |

The agent combines roles on a single task — a feature request engages the PM (requirements), Architect (design), Developer (code), Tester (tests), and PjM (tracking).

---

## Who Is This For

| You are... | Start here |
|-----------|-----------|
| A **team lead** evaluating AI agents | `PLAN.md` → `plan/00-overview.md` |
| An **engineer** building the agent | `plan/03-implementation-guide.md` |
| An **org adopting** for your team | `CUSTOMIZATION.md` |
| **Anyone** understanding a file/dir | `DIRECTORY_GUIDE.md` |

---

## Directory Structure

```
/
+-- README.md                        # This file
+-- LICENSE                          # MIT License — no strings attached
+-- PLAN.md                          # Master plan (7 phases, 24 weeks)
+-- CUSTOMIZATION.md                 # How to fork and adapt for your org
+-- DIRECTORY_GUIDE.md               # Purpose and usage of every file
|
+-- roles/                           # The 9 agent roles
|   +-- README.md                    # Role system overview and switching logic
|   +-- architect.md                 # Architect role definition
|   +-- developer.md                 # Developer role definition
|   +-- tester.md                    # Tester role definition
|   +-- ux-expert.md                 # UX Expert role definition
|   +-- product-manager.md           # Product Manager role definition
|   +-- project-manager.md           # Project Manager role definition
|   +-- program-manager.md           # Program Manager role definition
|   +-- data-scientist.md            # Data Scientist role definition
|   +-- customer-persona.md          # Customer Persona role definition
|
+-- domains/                         # Domain-specific knowledge (extensible)
|   +-- README.md                    # How domains work, how to add yours
|   +-- relevancy/                   # Reference domain: relevancy engineering
|       +-- overview.md
|       +-- skills.md
|       +-- evaluation.md
|       +-- workflows.md
|       +-- glossary.md
|
+-- plan/                            # Detailed planning documents
|   +-- 00-overview.md               # Vision, problem statement, goals
|   +-- 01-capabilities.md           # Capabilities organized by role
|   +-- 02-architecture.md           # System architecture with role routing
|   +-- 03-implementation-guide.md   # Step-by-step build instructions
|   +-- 04-foundational-skills.md    # Cross-role problem-solving skills
|   +-- 05-foundational-tools.md     # Full toolchain (OS through AI tools)
|   +-- phases/                      # Phase-by-phase implementation plans
|       +-- phase-1-cli-foundation.md
|       +-- phase-2-integrations.md       (Developer + Tester roles)
|       +-- phase-3-evaluation-engine.md  (Workflow integrations)
|       +-- phase-4-data-analysis.md      (Architect + Data Scientist)
|       +-- phase-5-documentation-automation.md (PM + UX roles)
|       +-- phase-6-ui-layer.md           (Domain + doc automation)
|       +-- phase-7-ui-layer.md           (Web interface)
|
+-- org/                             # Organization config (fill in when adopting)
|   +-- profile.md                   # Team context and mission
|   +-- infrastructure.md            # Tech stack decision record
|   +-- policies.md                  # Agent guardrails and boundaries
|
+-- tools/                           # AI tool capability guides
|   +-- claude-code/                 # Claude Code: setup, capabilities, workflows
|   +-- github-copilot/              # Copilot: IDE integration, workflows
|   +-- gemini-enterprise/           # Gemini: large-context analysis, workflows
|   +-- glean/                       # Glean: enterprise search, workflows
|
+-- agent-core/                      # Agent implementation (future code)
|   +-- cli/                         # CLI interface
|   +-- integrations/                # Jira, Confluence, Git integrations
|   +-- evaluations/                 # Domain evaluation framework
|   +-- data-analysis/               # Data analysis pipeline
|   +-- app-builder/                 # Application scaffolding
|
+-- templates/                       # Document generation templates
|   +-- confluence/                  # Confluence page templates
|   +-- jira/                        # Jira comment templates
|   +-- evaluation-reports/          # Evaluation output templates
|
+-- docs/                            # Team documentation
|   +-- guides/                      # How-to guides
|   +-- architecture/                # Architecture Decision Records
|
+-- config/                          # Runtime configuration
|
+-- prompts/                         # Prompts to recreate this entire framework
|   +-- README.md                    # How the prompt system works
|   +-- 00-master.md                 # Single prompt to generate everything
|   +-- 01-scaffold.md              # Directory structure and root files
|   +-- 02-roles.md                 # Generate 9 role definitions
|   +-- 03-domains.md               # Generate domain extension system
|   +-- 04-plan.md                  # Generate all plan documents
|   +-- 05-tools.md                 # Generate AI tool guides
|   +-- 06-org.md                   # Generate org configuration templates
|   +-- 07-templates.md             # Generate document templates
|   +-- 08-agent-config.md          # Generate agent configuration guide
|   +-- 09-documentation.md         # Generate README, guides, customization
```

---

## Quick Start

### Use as-is (with relevancy engineering domain)

```bash
git clone https://github.com/ilamgumaran/relevancyengineer.git
cd relevancyengineer
# Read: PLAN.md → plan/03-implementation-guide.md → roles/README.md
```

### Fork for your team

```bash
git clone https://github.com/YOUR_ORG/YOUR_FORK.git
cd YOUR_FORK

# 1. Define your org
vi org/profile.md org/infrastructure.md org/policies.md

# 2. Add your domain (or use relevancy as-is)
mkdir domains/your-domain
# Copy structure from domains/relevancy/

# 3. Follow the plan
# Read: CUSTOMIZATION.md → plan/03-implementation-guide.md
```

---

## How Roles Work

```
$ agent task --jira ENG-123 "Add user preference API"

[Product Manager] Reading requirements from ENG-123...
  Requirements: REST API for CRUD on user preferences
  Missing: Max preference size not specified → flagging

[Architect] Assessing design...
  Pattern: Follows existing API conventions in /api/v1/
  Storage: PostgreSQL (consistent with other entities)

[Developer] Implementing...
  Branch: feat/ENG-123-user-preferences
  Files: 3 new, 1 modified
  Tests: 12 (unit + integration)

[Tester] Validating...
  All tests passing ✓
  Coverage: 94% on new code
  Edge case flagged: empty preferences object

[Project Manager] Updating tracking...
  PR #204 created
  ENG-123 → In Review
  Confluence page updated
```

---

## Portability

| Environment | Works? | Notes |
|-------------|--------|-------|
| Cloud-native | Yes | GitHub/GitLab SaaS, K8s, cloud AI APIs |
| On-premise | Yes | Self-hosted git, K8s/bare-metal, Ollama/vLLM |
| Hybrid | Yes | Mix of cloud and on-prem |
| Air-gapped | Yes | Self-hosted everything, open models |

---

## License

MIT — use it, fork it, modify it, sell it, no strings attached.

---

## Contributing

Contributions welcome:
- **New roles**: Add to `roles/`
- **New domains**: Add to `domains/`
- **New tool guides**: Add to `tools/`
- **Framework improvements**: PRs against plan docs
- **Workflow recipes**: Add to relevant `workflows.md`

---

## Recreating This Framework

The `prompts/` directory contains structured prompts that can regenerate this entire framework from scratch. Feed `prompts/00-master.md` to an AI agent in an empty repo, or run the numbered prompts individually. See `prompts/README.md` for details.
