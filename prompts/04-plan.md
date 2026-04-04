# Prompt 04: Generate the Plan Documents

## Context

You are building a multi-role software engineering agent framework. The `roles/` directory defines 9 roles. The `domains/` directory has a reference domain. Now you need the planning documents that explain the vision, capabilities, architecture, implementation guide, foundational skills, foundational tools, and phase-by-phase execution plan.

## Objective

Create `PLAN.md` (root), and 6 plan documents in `plan/`, plus 7 phase files in `plan/phases/`.

## Instructions

### `PLAN.md` — Master Plan (root file)

A single-page executive summary:
- Goal statement (2 sentences: what we're building)
- 7 phases with name, week range, 2-sentence description, and key deliverables line
- Success criteria (10 items covering all 9 roles, traceability, and org adoption time)
- Key documents table linking to all plan files, roles, domains, and customization guide

### `plan/00-overview.md` — Vision and Overview

- **Vision**: 1 paragraph on why multi-role agents matter
- **Problem statement**: 6 numbered problems engineering teams face (role gaps, context switching, inconsistent quality, documentation lag, onboarding friction, tool fragmentation)
- **Solution**: 6 bullet points describing what the agent does (plays 9 roles, combines roles, works in your workflow, domain-extensible, org-configurable, documents as it works)
- **The 9 roles table**: Role name, what it does, when it activates (9 rows)
- **Goals table**: Goal, metric, target (7 rows covering multi-role completion, code quality, docs, onboarding, traceability, domain extensibility, org adoption)
- **Constraints**: 6 constraints (human-in-the-loop, security, auditability, cost, role honesty, domain boundaries)
- **Stakeholders table**: 7 rows (engineers, tech leads, managers, data scientists, PMs, new members, customers/end users)
- **Tool strategy table**: 4 tools (Claude Code, Copilot, Gemini, Glean) with role in agent

### `plan/01-capabilities.md` — Capabilities by Role

For EACH of the 9 roles (including Customer Persona), create a table with columns: Capability, Description, Tools Used. Each role should have 6-8 capabilities.

After the role tables, include:
- **CLI interface**: Show 10+ command examples with comments indicating which role activates
- **Explicit role selection**: Show `--role` flag usage
- **Role combination patterns**: Table with 8+ task types showing which roles engage in which order (including Customer Persona where applicable)

### `plan/02-architecture.md` — System Architecture

- **High-level architecture diagram** (ASCII art): CLI + Web UI → Task Router + Role Selector → Role Executors (including Customer Persona) → Integration Layer → External Systems (Git, Issues, Docs, Data)
- **Component details**: Task Router + Role Selector (with role selection logic pseudocode), Role Executors (how they share the same AI but different prompts), Integration Layer (platform-agnostic: Git, Issues, Docs, Data)
- **Data flow**: Numbered step-by-step showing a multi-role task from CLI input to final output (8+ steps, labeled with which role is active)
- **Technology stack table**: 12+ rows (CLI, AI orchestration, IDE assistant, large context, search, issues, docs, git, data, UI, task queue)
- **Security model**: ASCII box showing CAN (8 items) and CANNOT (5 items)
- **Role routing architecture**: ASCII diagram showing User Request → Intent Classifier → Single/Multi Role path → Role Executor(s) → Output → Integration Layer

### `plan/03-implementation-guide.md` — Step-by-Step Implementation

For each phase, provide detailed implementation steps. Each step MUST include:
1. **What**: One-sentence description
2. **How to implement**: Code examples, commands, or configuration snippets
3. **How Claude Code helps**: The exact prompt to give Claude Code
4. **Outcome**: What success looks like
5. **Verification**: How to confirm it works

Cover at minimum these steps:
- Phase 1: Python project setup, CLAUDE.md creation with role system, CLI commands, Claude Code integration (subprocess vs. API), local state management (SQLite), MCP server config, memory seeding
- Phase 2: Code generation patterns, test generation patterns, code review workflow
- Phase 3: Issue tracker MCP server, documentation MCP server, git automation, cross-references
- Phase 4: System design output format, ADR generation, data connectors, analysis library
- Phase 5: User story generation, sprint planning, UX review workflow
- Phase 6: Domain loading, template engine, auto-documentation triggers
- Phase 7: REST API, web UI

End with a **dependency table**: Step, What, Depends On, Primary Tool (20+ rows)

### `plan/04-foundational-skills.md` — Cross-Role Problem-Solving

Structure around the 8-stage journey (these stages are universal across all roles):

1. **Problem Understanding** (PM, UX): stakeholder communication, problem classification table (8 types → roles), context gathering
2. **Problem Diagnosis** (Dev, Architect, DS): systematic investigation, technical diagnostics table (7+ tools), data-driven diagnosis
3. **Root Cause Analysis** (Dev, Architect): causal reasoning (5 Whys, fault tree), system thinking
4. **Solution Design** (Architect, PM, Dev): option generation, tradeoff analysis table (7 dimensions), decision making
5. **Implementation** (Dev, Tester): software craftsmanship, cross-language proficiency table (8 languages), version control discipline
6. **Validation** (Tester, Dev): multi-level validation table (8 levels), regression awareness
7. **Impact Measurement** (DS, PM, PjM): metric selection, statistical rigor, business translation
8. **Documentation** (all): documentation types table (8 types by role), knowledge management

End with:
- **Cross-cutting skills**: Communication, collaboration, continuous learning
- **Skill maturity model**: 4 levels (Executor → Analyst → Strategist → Expert) with descriptions

### `plan/05-foundational-tools.md` — Infrastructure Toolchain

Structure as 8 layers:

- **Layer 0: OS/Hardware**: Bare-metal vs. VM vs. container vs. serverless spectrum with decision matrix (5 factors × 4 options). Include prompt-to-compiled-code pattern for performance-critical components.
- **Layer 1: Source Control**: Git core skills table (10 operations), branching strategies table (4 strategies), git hosting platforms table (5+), code review patterns
- **Layer 2: Dev Environment**: Native, dev containers (with devcontainer.json example), cloud IDEs table (5+), AI-optimized prompt-to-binary workflow
- **Layer 3: Runtime**: Docker (with Dockerfile example), Kubernetes concepts, alternatives table (6+), bare-metal service management
- **Layer 4: CI/CD**: CI platforms table (8+), example GitHub Actions pipeline for the agent, deployment strategies table (5), testing pyramid for search/domain with table (8 test types)
- **Layer 5: Observability**: Logging tools table (5+), metrics tools table (5+), tracing tools table (5+), domain-specific alerting table (5 signals)
- **Layer 6: Workflow**: Issue tracking tools table (7+), documentation tools table (7+), communication tools table (4+)
- **Layer 7: AI Tools**: Code generation tools table (7+), enterprise knowledge tools table (4+)

Each layer must have an "Organization Extension Point" marker.

End with:
- **Infrastructure Decision Record template** (comprehensive, covering all layers)
- **Portability matrix**: 4 environments (cloud, on-prem, hybrid, air-gapped) × 6 components
- **Fully air-gapped stack**: Complete self-hosted alternative for every component

### Phase Files (`plan/phases/phase-N-*.md`)

Create 7 phase files. Each phase file MUST include:
1. **Objective**: 1-2 sentences
2. **Deliverables**: Numbered list with 3-6 deliverables, each with a short description
3. **Verification checklist**: 6-8 checkbox items that define "done"

The 7 phases:
1. **Core Agent Foundation** (Weeks 1-3): CLI, role switching, CLAUDE.md, MCP servers, memory
2. **Developer + Tester Roles** (Weeks 4-6): Code gen/mod, debugging, test gen, quality gates, code review
3. **Workflow Integrations** (Weeks 7-9): Issue tracker, docs platform, git automation, cross-references
4. **Architect + Data Scientist** (Weeks 10-12): System design, ADRs, data analysis, experiments
5. **PM + UX + Customer Persona Roles** (Weeks 13-15): User stories, sprint planning, program management, UX review, customer persona simulation
6. **Domain + Doc Automation** (Weeks 16-18): Domain extension, auto-docs, knowledge base
7. **UI Layer** (Weeks 19-24): REST API, web app, auth

## Quality Criteria

- Plan documents should reference each other (hyperlinks between files)
- Architecture should include at least 2 ASCII diagrams
- Implementation guide should have enough detail that someone can follow it mechanically
- Foundational tools should cover both cloud-native AND air-gapped scenarios
- Phase files should be concise (30-60 lines each) — the detail is in the implementation guide

## Verification

- `PLAN.md` and 6 files exist in `plan/`
- 7 files exist in `plan/phases/`
- Implementation guide has 20+ steps with code examples
- Foundational tools covers all 8 layers with tables
- Every phase has a verification checklist
- Commit with message: "Add comprehensive plan documents with 7-phase roadmap"
