# HIO-Based Engineering Org Setup

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

How to **set up and run an engineering organization on HIO principles** -- purpose definition, role taxonomy, goals, effectiveness measures, and the transformation plan that gets you from where you are to a functioning HIO-aligned engineering org. This repo is the structural template; fork it, fill in your org's context, and run.

The day-to-day agentic toolkit that operates *inside* such an org lives downstream in [`software-engineering-hio-agent-framework`](https://github.com/ilamgumaran/software-engineering-hio-agent-framework).

---

## Where this sits in the family

| # | Layer | Repo | What it is |
|---|---|---|---|
| 1 | Cognition foundation | [`thoughtexperiments`](https://github.com/ilamgumaran/thoughtexperiments) | Resonant Cognition -- a psychology-of-mind theory |
| 2 | Generalized HIO framework | [`thought-org-with-human-ai-hybrid`](https://github.com/ilamgumaran/thought-org-with-human-ai-hybrid) | Orchestrating organic + inorganic intelligence at any scale, built on cognition principles |
| 3 | **Engineering org applied** (this repo) | `software-engineer-core-structure` | Setting up an engineering organization on HIO principles -- roles, goals, effectiveness measures, transformation plan |
| 4 | Day-to-day agentic toolkit | [`software-engineering-hio-agent-framework`](https://github.com/ilamgumaran/software-engineering-hio-agent-framework) | The main agentic workflow toolkit used inside such an HIO-aligned engineering org |

This repo applies HIO methodology to the specific case of engineering organizations. The 9 roles below are the role taxonomy used when setting up such an org; goals and effectiveness measures here track whether the org is delivering on HIO's principles.

---

## The 9 Roles

The role taxonomy used when setting up an HIO-aligned engineering organization. The agent built from this template can switch between any of these roles based on the task; humans in the org typically hold a primary role plus one or two adjacent ones.

| Role | What it does |
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

A single feature request will engage several roles -- PM (requirements), Architect (design), Developer (code), Tester (tests), Project Manager (tracking). Under HIO, the same person may *hold* multiple roles in a session; the relevant unit of work is outcome, not job title.

---

## Goals and effectiveness measures

An HIO-aligned engineering org is measured against the **4 Core Principles** of HIO ([upstream](https://github.com/ilamgumaran/thought-org-with-human-ai-hybrid#core-principles)):

1. **Purpose as a Living Force** -- can every team member explain the org's purpose in their own words and connect their work to it?
2. **Harmonize, Don't Divide** -- are humans and AI organized around outcomes, not separate territories?
3. **Fulfillment as the Engine** -- is human fulfillment measured alongside delivery, and acted on?
4. **Measure the Whole Ecosystem** -- is no metric optimized while another silently degrades?

Concrete instruments per principle, plus the role-by-role goals each role contributes to, are detailed in `plan/` and the goals templates in `org/`. The transformation plan (below) is the path that takes an existing or new org to passing all four checks.

---

## Who Is This For

| You are... | Start here |
|-----------|-----------|
| A **leader** setting up or restructuring an engineering org on HIO | `PLAN.md` then `plan/00-overview.md` |
| An **engineer** in such an org wanting to understand the structure | `roles/README.md` |
| An **org adopting** for your team | `CUSTOMIZATION.md` |
| **Anyone** understanding a file/dir | `DIRECTORY_GUIDE.md` |

---

## Directory Structure

```
/
+-- README.md                        # This file
+-- LICENSE                          # MIT License -- no strings attached
+-- AGENTS.md                        # Guidance for AI agents working in this repo
+-- PLAN.md                          # Transformation plan
+-- CUSTOMIZATION.md                 # How to fork and adapt for your org
+-- DIRECTORY_GUIDE.md               # Purpose and usage of every file
|
+-- roles/                           # The 9 roles -- HIO-aligned engineering org taxonomy
|   +-- README.md                    # Role system overview and switching logic
|   +-- architect.md
|   +-- developer.md
|   +-- tester.md
|   +-- ux-expert.md
|   +-- product-manager.md
|   +-- project-manager.md
|   +-- program-manager.md
|   +-- data-scientist.md
|   +-- customer-persona.md
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
|
+-- org/                             # Organization config (fill in when adopting)
|   +-- profile.md                   # Team context and mission
|   +-- infrastructure.md            # Tech stack decision record
|   +-- policies.md                  # Agent guardrails and boundaries
|
+-- tools/                           # AI tool capability guides
|   +-- claude-code/
|   +-- github-copilot/
|   +-- gemini-enterprise/
|   +-- glean/
|
+-- agent-core/                      # Agent implementation (future code)
|
+-- templates/                       # Document generation templates
+-- docs/                            # Team documentation
+-- config/                          # Runtime configuration
+-- prompts/                         # Prompts to recreate this entire framework
```

---

## Quick Start

### Fork for your team

```bash
git clone https://github.com/YOUR_ORG/YOUR_FORK.git
cd YOUR_FORK

# 1. Read upstream HIO methodology to ground yourself
#    https://github.com/ilamgumaran/thought-org-with-human-ai-hybrid

# 2. Define your org
vi org/profile.md org/infrastructure.md org/policies.md

# 3. Add your domain (or use relevancy as-is)
mkdir domains/your-domain
# Copy structure from domains/relevancy/

# 4. Follow the plan
# Read: CUSTOMIZATION.md -> plan/03-implementation-guide.md

# 5. Adopt the day-to-day agentic toolkit
#    https://github.com/ilamgumaran/software-engineering-hio-agent-framework
```

---

## How Roles Work

```
$ agent task --jira ENG-123 "Add user preference API"

[Product Manager] Reading requirements from ENG-123...
  Requirements: REST API for CRUD on user preferences
  Missing: Max preference size not specified -> flagging

[Architect] Assessing design...
  Pattern: Follows existing API conventions in /api/v1/
  Storage: PostgreSQL (consistent with other entities)

[Developer] Implementing...
  Branch: feat/ENG-123-user-preferences
  Files: 3 new, 1 modified
  Tests: 12 (unit + integration)

[Tester] Validating...
  All tests passing
  Coverage: 94% on new code

[Project Manager] Updating tracking...
  PR #204 created
  ENG-123 -> In Review
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

## Relationship to the rest of the family

- **Upstream** -- the HIO methodology this repo applies lives in [`thought-org-with-human-ai-hybrid`](https://github.com/ilamgumaran/thought-org-with-human-ai-hybrid). Read it first to ground yourself in the principles.
- **Cognition source** -- HIO itself rests on a theory of cognition; that theory lives in [`thoughtexperiments`](https://github.com/ilamgumaran/thoughtexperiments) (Resonant Cognition Framework).
- **Downstream** -- once your engineering org is set up on HIO, the day-to-day agentic toolkit lives in [`software-engineering-hio-agent-framework`](https://github.com/ilamgumaran/software-engineering-hio-agent-framework). It supplies the 6 agent types, sprint ceremonies, and multi-repo orchestration.

This repo and the day-to-day toolkit overlap in places (cognitive functions, units, metrics, transformation phases were originally drafted in the toolkit repo). The canonical home for **org-setup** content is here; the canonical home for **agent operation** is downstream. Where overlap exists, both repos cross-link so consumers find one source of truth.

---

## License

MIT -- use it, fork it, modify it, sell it, no strings attached.

---

## Contributing

Contributions welcome:
- **New roles**: Add to `roles/`
- **New domains**: Add to `domains/`
- **New tool guides**: Add to `tools/`
- **Goals/measures additions**: PR against the plan documents
- **Workflow recipes**: Add to relevant `workflows.md`

---

## Recreating This Framework

The `prompts/` directory contains structured prompts that can regenerate this entire framework from scratch. Feed `prompts/00-master.md` to an AI agent in an empty repo, or run the numbered prompts individually. See `prompts/README.md` for details.
