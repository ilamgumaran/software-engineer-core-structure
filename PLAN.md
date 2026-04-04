# Master Plan: Multi-Role Software Engineering Agent

## Goal

Build an AI agent that operates as a multi-role software engineering team member — switching between architect, developer, tester, UX expert, product manager, project manager, program manager, data scientist, and customer persona as tasks require. The agent works within your team's existing workflow (git, issue tracker, documentation platform) and is configurable for any engineering domain.

---

## Phases Overview

### Phase 1: Core Agent Foundation (Weeks 1-3)
Build the CLI interface, role-switching system, and AI tool configuration. Establish Claude Code as the execution engine with project context, memory, and role definitions.

**Key deliverables**: Working CLI, role selection system, CLAUDE.md configuration, basic task routing across roles

---

### Phase 2: Developer + Tester Roles (Weeks 4-6)
Implement the two most hands-on roles — the developer who writes and modifies code, and the tester who validates it. These form the inner loop of the agent's work.

**Key deliverables**: Code generation, test generation, bug fixing, code review, test execution, quality gate enforcement

---

### Phase 3: Workflow Integrations (Weeks 7-9)
Connect the agent to the team's issue tracker (Jira/Linear), documentation platform (Confluence/Notion), and git hosting (GitHub/GitLab). Enable the agent to operate within existing workflows, not alongside them.

**Key deliverables**: Issue reading/updating, documentation creation, structured git operations, cross-referencing

---

### Phase 4: Architect + Data Scientist Roles (Weeks 10-12)
Implement the analytical roles — the architect who designs systems and evaluates tradeoffs, and the data scientist who analyzes data and builds models.

**Key deliverables**: System design outputs, ADR generation, data analysis pipeline, experiment design, metric calculation

---

### Phase 5: PM + UX Roles (Weeks 13-15)
Implement the product-facing roles — product manager (requirements, prioritization), project manager (planning, tracking), program manager (cross-team), and UX expert (design, accessibility).

**Key deliverables**: User story writing, sprint planning, roadmap management, UX review, accessibility audit

---

### Phase 6: Domain Layer + Documentation Automation (Weeks 16-18)
Build the domain extension system and documentation automation. Enable organizations to plug in their specific domain knowledge and have documentation generated as a side effect of work.

**Key deliverables**: Domain template system, auto-generated docs, knowledge base, evaluation framework

---

### Phase 7: UI Layer (Weeks 19-24)
Build a web interface for task assignment, progress tracking, conversation, and reporting.

**Key deliverables**: REST API, web app, task dashboard, conversation interface

---

## Success Criteria

1. Team members can assign any engineering task via CLI and the agent selects the right role(s)
2. The agent produces working, tested code from a Jira story (Developer + Tester)
3. The agent designs system architectures with ADRs (Architect)
4. The agent analyzes data and reports insights with statistical rigor (Data Scientist)
5. The agent writes user stories with acceptance criteria (Product Manager)
6. The agent plans sprints and tracks progress (Project Manager)
7. The agent reviews UI for usability and accessibility (UX Expert)
8. The agent coordinates cross-team dependencies (Program Manager)
9. The agent models end-user behavior and validates features from the customer perspective (Customer Persona)
10. Every action is traceable — git commits, issue updates, documentation
11. Organizations can fork and customize for their domain in <1 day

---

## Key Documents

| Document | Purpose |
|----------|---------|
| `plan/00-overview.md` | Vision, problem statement, goals |
| `plan/01-capabilities.md` | Capabilities organized by role |
| `plan/02-architecture.md` | System architecture with role routing |
| `plan/03-implementation-guide.md` | Step-by-step build instructions |
| `plan/04-foundational-skills.md` | Cross-role problem-solving skills |
| `plan/05-foundational-tools.md` | Full toolchain at every layer |
| `roles/` | Detailed definition of each role |
| `domains/` | Domain-specific knowledge (extensible) |
| `CUSTOMIZATION.md` | How to fork and adapt for your org |
