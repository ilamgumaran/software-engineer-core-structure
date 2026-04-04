# Plan Overview: Multi-Role Software Engineering Agent

## Vision

Software engineering teams need team members who can flex across roles — an architect in the morning, a developer in the afternoon, a tester before merging, a project manager when reporting. AI agents can fill this need, but today they're typically narrow: a coding assistant that only writes code, or a planning tool that only tracks tasks.

This framework creates a **multi-role engineering agent** that switches between 9 roles based on the task at hand, works within the team's existing workflow, and can be customized for any engineering domain.

## Problem Statement

Engineering teams face:

1. **Role gaps**: Not every team has a dedicated architect, data scientist, UX expert, or program manager. Knowledge gets concentrated in individuals who become bottlenecks.
2. **Context switching**: An engineer asked to "also handle project management" loses hours switching between coding, Jira, Confluence, and stakeholder communication.
3. **Inconsistent quality**: Without a tester's adversarial mindset, edge cases get missed. Without an architect's systems thinking, designs accumulate tech debt. Without a PM's user focus, features miss the mark.
4. **Documentation lag**: Nobody's job is to document, so documentation falls behind reality.
5. **Onboarding friction**: New team members take weeks to understand the codebase, processes, and decision history because knowledge is tribal.
6. **Tool fragmentation**: Each AI tool (Copilot, Claude, Gemini, Glean) has strengths, but nobody orchestrates them together for end-to-end task completion.

## Solution

An AI agent that:

- **Plays 9 roles** — Architect, Developer, Tester, UX Expert, Product Manager, Project Manager, Program Manager, Data Scientist, Customer Persona — switching as the task requires
- **Combines roles on a single task** — A feature request engages the PM (requirements), Architect (design), Developer (code), Tester (validation), and PjM (tracking)
- **Works within your workflow** — Reads issues, updates status, commits code, creates docs in your existing tools
- **Is domain-extensible** — Relevancy engineering, ML platform, backend, frontend, data engineering — plug in your domain knowledge
- **Is org-configurable** — Your tools, your policies, your guardrails, your conventions
- **Documents as it works** — Every action produces a trail: git commits, issue comments, wiki pages

## The 9 Roles

| Role | What It Does | When It Activates |
|------|-------------|-------------------|
| **Architect** | Designs systems, evaluates tradeoffs, ensures technical coherence | System design, tech selection, migration planning |
| **Developer** | Writes, modifies, and debugs code across the stack | Feature implementation, bug fixes, refactoring |
| **Tester** | Validates correctness, finds edge cases, ensures quality | Test writing, regression testing, quality gates |
| **UX Expert** | Designs user experiences, advocates for usability | UI design, usability review, accessibility |
| **Product Manager** | Defines what to build and why, manages requirements | Feature scoping, user stories, prioritization |
| **Project Manager** | Plans execution, tracks progress, manages risks | Sprint planning, status reports, blockers |
| **Program Manager** | Coordinates across teams, manages dependencies | Cross-team alignment, portfolio management |
| **Data Scientist** | Analyzes data, builds models, extracts insights | Data analysis, experiments, metric definition |
| **Customer Persona** | Simulates customer reactions, validates UX from user perspectives, predicts behavior | User validation, persona testing, behavior prediction |

## Goals

| Goal | Metric | Target |
|------|--------|--------|
| Multi-role task completion | % of tasks where agent correctly applies 2+ roles | >80% |
| Code quality | % of agent PRs that pass review without changes | >70% |
| Documentation coverage | % of features with up-to-date docs | >90% |
| Onboarding acceleration | Time for new engineer to complete first task | <1 day |
| Cross-role consistency | % of tasks with proper traceability (git+issue+docs) | >95% |
| Domain extensibility | Time to configure agent for a new domain | <1 day |
| Org adoption | Time to fork and configure for a new organization | <4 hours |

## Constraints

- **Human-in-the-loop**: Code merges, architecture decisions, and production changes require human approval
- **Security**: The agent never has production write access. All actions go through review processes.
- **Auditability**: Every action is traceable through git, issue tracker, and documentation platform
- **Cost awareness**: AI API usage has costs. The agent batches operations and avoids unnecessary calls.
- **Role honesty**: The agent states which role it's operating in and why, making its reasoning transparent
- **Domain boundaries**: The agent operates within its configured domain expertise. It escalates when outside its knowledge.

## Stakeholders

| Role | Interaction with Agent |
|------|----------------------|
| Engineers | Primary users — assign tasks, review outputs, ask questions |
| Tech Leads | Review architecture decisions, approve designs |
| Engineering Managers | Review progress reports, set priorities |
| Data Scientists | Collaborate on analysis, validate models |
| Product Managers | Define requirements, review against acceptance criteria |
| New Team Members | Ask onboarding questions, learn the codebase |

## Tool Strategy

| Tool | Role in the Agent |
|------|------------------|
| **Claude Code** | Core execution engine — all 9 roles operate through it |
| **GitHub Copilot** | In-IDE assistant for engineers doing hands-on work alongside the agent |
| **Gemini Enterprise** | Large-context analysis, bulk LLM operations, Google Workspace integration |
| **Glean** | Enterprise knowledge search across all tools |
