# Master Prompt: Generate the Multi-Role Software Engineering Agent Framework

## Who You Are

You are an AI coding agent creating a comprehensive framework for building multi-role software engineering agents. You will generate an entire repository of planning documents, role definitions, domain knowledge, tool guides, organizational templates, document templates, and documentation.

## What You Are Building

A **structural plan and prompt system** that any engineering team — small or large — can fork and customize to create an AI agent that plays 9 roles:

1. **Architect** — Designs systems, evaluates tradeoffs, produces ADRs
2. **Developer** — Writes, modifies, and debugs code across the stack
3. **Tester** — Validates correctness, finds edge cases, ensures quality
4. **UX Expert** — Designs experiences, audits accessibility, advocates for users
5. **Product Manager** — Defines what to build and why, writes requirements
6. **Project Manager** — Plans sprints, tracks progress, manages risks
7. **Program Manager** — Coordinates across teams, manages dependencies
8. **Data Scientist** — Analyzes data, builds models, designs experiments
9. **Customer Persona** — Simulates customer reactions, validates UX from user perspectives, predicts behavior

The agent switches roles based on the task and combines multiple roles on a single task. It works within the team's existing workflow (git, issue tracker, documentation platform) and is configurable for any engineering domain.

The **reference domain** is relevancy engineering (search ranking quality), but the framework is domain-agnostic.

## Core Design Principles

1. **Roles are universal, domains are specific.** The 9 roles apply to any engineering team. Domain knowledge is a pluggable layer.
2. **Everything is a reviewable file.** Role definitions, policies, domain knowledge, agent behavior — all version-controlled markdown that goes through PR review.
3. **Organization-configurable.** Teams fork the repo and fill in their tools, conventions, policies, and domain. The framework has explicit extension points.
4. **Multi-environment.** Works on cloud, on-prem, hybrid, or air-gapped. Every tool recommendation comes with alternatives.
5. **MIT licensed.** No restrictions. Fork it, sell it, modify it.

## What to Generate

Generate the following files in this exact order. Each section below specifies the file path, purpose, and content requirements.

---

### Phase 1: Scaffold

**Create these directories** (all empty at first, content added in later phases):

```
roles/
domains/
domains/relevancy/
plan/
plan/phases/
tools/claude-code/
tools/github-copilot/
tools/gemini-enterprise/
tools/glean/
org/
agent-core/cli/
agent-core/integrations/jira/
agent-core/integrations/confluence/
agent-core/integrations/git/
agent-core/evaluations/
agent-core/data-analysis/
agent-core/app-builder/
docs/guides/
docs/architecture/
templates/confluence/
templates/jira/
templates/evaluation-reports/
config/
prompts/
```

**Create `.gitignore`**: Python, IDE, env, OS, Node patterns.
**Create `LICENSE`**: MIT, current year, "Multi-Role Software Engineering Agent Framework Contributors".

---

### Phase 2: Role Definitions

**Create `roles/README.md`**: Role system overview. Explain how role selection works, role switching (agent states which role is active), role combinations. Include a table mapping 8+ common task types to their role sequences. Include a role index table linking to all 9 files.

**Create 9 role files** (`roles/architect.md`, `roles/developer.md`, `roles/tester.md`, `roles/ux-expert.md`, `roles/product-manager.md`, `roles/project-manager.md`, `roles/program-manager.md`, `roles/data-scientist.md`, `roles/customer-persona.md`).

Each role file MUST have these exact sections:
- **Identity**: What the role does. When the agent activates it.
- **Perspective**: 5 questions the role asks. 5 things the role avoids.
- **Core Skills**: 3-6 skill categories with tables of specific techniques.
- **Decision Framework**: Numbered steps for decision-making.
- **Inputs and Outputs**: What it consumes from other roles, what it produces.
- **How the Agent Performs This Role**: Concrete example with command and step-by-step behavior.

Role-specific content requirements:
- Architect: tradeoff dimensions table, 8+ architecture patterns
- Developer: full-stack competence table by layer, code quality principles
- Tester: test pyramid diagram, edge case table with 8+ categories
- UX Expert: 6 design principles table, accessibility requirements
- Product Manager: INVEST checklist, 6+ prioritization frameworks table
- Project Manager: tracking table (6 items), risk management process
- Program Manager: dependency types table (5), stakeholder communication patterns
- Data Scientist: ML techniques table by category, experimentation methodology
- Customer Persona: 5 persona dimensions, reaction prediction table, journey simulation, 3 worked examples, persona templates, anti-patterns

---

### Phase 3: Domain Extension System

**Create `domains/README.md`**: What domains are, standard file structure (5 files), example domains table (8+), how to add a new domain.

**Create `domains/relevancy/overview.md`**: What relevancy engineering is, key concepts table (10+ terms), business impact, primary roles, multi-role execution example.

**Create `domains/relevancy/skills.md`**: Search pipeline table (8+ components with function and failure modes), ranking algorithms (6), evaluation methodology, problem decomposition tree (6+ branches), search engine proficiency.

**Create `domains/relevancy/evaluation.md`**: Metrics table (6 metrics), business metrics connection, business metrics table (6+), evaluation test suite YAML example, A/B testing methodology.

**Create `domains/relevancy/workflows.md`**: 4 multi-role workflows (diagnose problem, run evaluation, tune config, build feature) with explicit role labels at each step.

**Create `domains/relevancy/glossary.md`**: 25+ terms defined.

---

### Phase 4: Plan Documents

**Create `PLAN.md`** (root): Executive summary with 7 phases (weeks, description, deliverables), 10 success criteria, key documents table.

**Create `plan/00-overview.md`**: Vision, 6 problems, solution (6 bullets), 9-role table, goals table (7 rows), constraints (6), stakeholders (6), tool strategy (4 tools).

**Create `plan/01-capabilities.md`**: Capability table per role (6-8 capabilities each, 9 roles = 55+ total), CLI interface (10+ commands), role combination patterns table (8+ rows).

**Create `plan/02-architecture.md`**: High-level ASCII architecture diagram, component details (task router with role selection pseudocode, role executors, integration layer), multi-role data flow (8+ steps), technology stack table (12+ rows), security model (CAN/CANNOT), role routing ASCII diagram.

**Create `plan/03-implementation-guide.md`**: Step-by-step implementation for all 7 phases. Each step has: What, How (with code), How Claude Code helps (exact prompt), Outcome, Verification. 20+ steps total. End with dependency table.

**Create `plan/04-foundational-skills.md`**: 8-stage problem-solving journey (Problem Understanding → Diagnosis → Root Cause → Solution Design → Implementation → Validation → Impact → Documentation). Each stage: active roles, 2-3 skill areas with tables. End with cross-cutting skills and 4-level maturity model.

**Create `plan/05-foundational-tools.md`**: 8 infrastructure layers (OS/Hardware, Source Control, Dev Environment, Runtime, CI/CD, Observability, Workflow, AI Tools). Each layer: options with tables, decision matrices, "Organization Extension Point" markers. End with Infrastructure Decision Record template, portability matrix, air-gapped stack.

**Create 7 phase files** in `plan/phases/`:
1. Core Agent Foundation (Weeks 1-3): CLI, roles, CLAUDE.md, MCP, memory
2. Developer + Tester (Weeks 4-6): Code gen, tests, debugging, review
3. Workflow Integrations (Weeks 7-9): Issues, docs, git, cross-refs
4. Architect + Data Scientist (Weeks 10-12): Design, ADRs, analysis, experiments
5. PM + UX (Weeks 13-15): Stories, planning, coordination, accessibility
6. Domain + Doc Automation (Weeks 16-18): Domain system, auto-docs, knowledge base
7. UI Layer (Weeks 19-24): REST API, web app, auth

Each phase file: Objective, 3-6 deliverables with descriptions, verification checklist (6-8 items).

---

### Phase 5: Tool Guides

For each of 4 tools (Claude Code, GitHub Copilot, Gemini Enterprise, Glean), create:

**`tools/<tool>/README.md`**: What it is, 3-6 key capabilities with examples, comparison table (when to use this vs. others, 10+ rows), setup guide (3-6 steps), limitations (5 items).

**`tools/<tool>/workflows.md`**: 4-8 concrete workflow recipes with trigger, numbered steps.

Claude Code README must include: CLAUDE.md integration, memory, MCP servers (with JSON config), hooks, subagents, architecture diagram.

---

### Phase 6: Organizational Templates

**Create `org/profile.md`**: Fillable template with [bracket placeholders] for team, mission, customers, systems, metrics, constraints, dependencies.

**Create `org/infrastructure.md`**: Fillable template covering 10 infrastructure categories (source control through security), all with [bracket placeholders].

**Create `org/policies.md`**: Fillable template with checkbox lists for data policies, code policies, workflow policies, quality guardrails, escalation policies.

---

### Phase 7: Document Templates

**Create `templates/confluence/evaluation-report.md.j2`**: Jinja2 template with metrics loop table, conditional regressions/improvements, variables for all dynamic content.

**Create `templates/confluence/progress-update.md.j2`**: Jinja2 template with task loops, findings, metrics table, next steps.

**Create `templates/jira/task-comment.md.j2`**: Jinja2 template with conditional sections for branch, PR, docs, evaluation, next steps.

---

### Phase 8: Agent Configuration Guide

**Create `docs/guides/agent-configuration.md`**: Guide for creating CLAUDE.md. Include: complete CLAUDE.md template with role system, 3 role integration examples, MCP server config JSON (4 servers), 10+ memory seeding commands, 3 hook examples, customization checklist (11 items).

---

### Phase 9: Documentation

**Create `README.md`**: MIT badge, one-paragraph description, 9-role table, who-is-this-for table, full directory tree, quick start (use as-is + fork), multi-role execution example, portability table, contributing guidelines.

**Create `DIRECTORY_GUIDE.md`**: Purpose, how-to-use, and when-to-modify for EVERY file and directory. Organized by directory. End with summary table (12+ rows).

**Create `CUSTOMIZATION.md`**: Adoption guide (7 steps: fork → profile → infra → roles → domain → policies → CLAUDE.md), extension points, domain template, example domains table, policy template with enforcement mechanisms, scaling patterns (single team → multi-team → org-wide), config-as-code table, getting started checklist.

---

## After Generation

1. Run `git add -A && git status` to verify all files
2. Commit with: "Generate multi-role software engineering agent framework"
3. Verify: count files (should be 40+), check each directory has content, spot-check 3 role files for correct structure

## Quality Standards

- Every table must have 4+ rows of specific, actionable content
- Every code example must be syntactically correct
- Every file must be self-contained enough to be useful without reading other files first
- Cross-references between files must use correct relative paths
- No placeholder content — every section must have real, substantive content
- Domain-agnostic in the framework layer, domain-specific only in `domains/`
