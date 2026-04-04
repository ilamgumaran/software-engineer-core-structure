# Prompt 06: Generate Organization Configuration Templates

## Context

You are building a multi-role software engineering agent framework. The framework must be adoptable by any organization. The `org/` directory contains templates that teams fill in to configure the agent for their specific context.

## Objective

Create 3 template files in `org/` that serve as fillable configuration for any adopting organization.

## Instructions

### `org/profile.md` — Team Profile Template

A fillable template with these sections:

1. **Team**: Name, domain, team size, key roles (as `[placeholder]` values)
2. **Mission**: Placeholder for team charter
3. **Customers**: Internal and external stakeholder placeholders
4. **Key Systems**: Table with System, Purpose, Technology columns (3 placeholder rows)
5. **Success Metrics**: Table with Metric, Current, Target, Why It Matters columns (2 placeholder rows)
6. **Constraints**: 3 placeholder bullet points with example types
7. **External Dependencies**: Table with Dependency, Owner, SLA, Impact columns

All values should be `[bracket placeholders]` that make it obvious what to fill in. Include a note at the top: "Replace this file with your organization's specific context."

### `org/infrastructure.md` — Infrastructure Decision Record

A comprehensive fillable template covering every infrastructure layer. Sections:

1. **Source Control**: Platform, branching strategy, default branch, protection rules (approvals, CI checks, linear history), merge method
2. **Development Environment**: Standard setup, required tools (with version placeholders), setup automation, IDE, extensions
3. **Languages and Frameworks**: Primary language(s), framework(s), package manager, linting, formatting, type checking
4. **Runtime and Deployment**: Deployment target, container registry, performance-critical components, service mesh, config management
5. **CI/CD**: Platform, deployment strategy, required gates (checkbox list: unit tests, integration tests, linting, security scan, domain evaluation), pipeline description
6. **Observability**: Logging, metrics, tracing, alerting tools, key dashboards
7. **Workflow Tools**: Issue tracking, documentation, communication platforms with URLs
8. **Data Infrastructure**: Data warehouse, search engine, cache, message queue, object storage
9. **AI Tools**: Approved tools, data governance restrictions, API access method, self-hosted models
10. **Network and Security**: Network access, authentication, secret management, compliance requirements

Every field should be a `[bracket placeholder]` with the category of expected value.

### `org/policies.md` — Agent Policies and Guardrails

A comprehensive template with checkbox lists the org checks off. Sections:

1. **Data Policies**:
   - What the agent CAN access (5 checkbox items: source code, non-prod DBs, public docs, anonymized data, CI logs)
   - What the agent CANNOT access (5 items: prod DBs, PII, secrets, financial data, other teams' repos)
   - What the agent CANNOT send to external AI APIs (5 items: customer data, tokens, architecture diagrams, unreleased info, HR/legal docs)

2. **Code Policies**:
   - What the agent CAN do (5 items: feature branches, commits, PRs, tests, docs)
   - What the agent CANNOT do (6 items: merge PRs, push to main, modify CI without review, delete branches, disable tests, add deps without review)

3. **Workflow Policies**:
   - CAN do (4 items: update status, add comments, create doc pages, post updates)
   - CANNOT do (5 items: close issues, modify other teams', delete pages, DM without asking, modify alerts)

4. **Quality Guardrails**:
   - Before any code change (4 checkbox items)
   - Before any domain-specific change (4 checkbox items)

5. **Escalation Policies**:
   - When the agent must escalate to a human (7 checkbox items)

Include a note at the top: "Replace this file with your organization's specific policies."

## Quality Criteria

- Templates must be immediately usable — copy, fill in brackets, done
- Every section should have enough placeholder rows/items that the team knows the expected depth
- Field names should be self-explanatory (no jargon that requires reading another doc)
- Checkbox items should cover the most common cases (teams can add more)

## Verification

- 3 files exist in `org/`
- `org/infrastructure.md` covers all 10 infrastructure categories
- `org/policies.md` has 5 policy sections with checkbox lists
- All placeholder values use `[bracket]` format
- Commit with message: "Add organization configuration templates for profile, infrastructure, policies"
