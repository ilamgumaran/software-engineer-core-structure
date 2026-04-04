# Prompt 09: Generate Documentation Files

## Context

You are building a multi-role software engineering agent framework. All content exists (roles, domains, plan, tools, org, templates, agent config guide). Now you need the user-facing documentation that ties everything together — README, DIRECTORY_GUIDE, and CUSTOMIZATION guide.

## Objective

Create 3 root-level documentation files: `README.md`, `DIRECTORY_GUIDE.md`, `CUSTOMIZATION.md`.

## Instructions

### `README.md` — Project Front Door

The README must make the project instantly understandable. Structure:

1. **Title**: "Multi-Role Software Engineering Agent Framework"
2. **Badge**: MIT License badge (shields.io)
3. **One-paragraph description**: What it is, 9 roles, forkable, domain-agnostic, both plan and prompt
4. **The 9 Roles table**: Role name, what it does (9 rows, including Customer Persona)
5. **Who Is This For table**: 4 audiences (team lead, engineer, org adopting, anyone) → where to start
6. **Directory Structure**: Full tree showing every directory and key file with inline comments
7. **Quick Start**: Two paths — "use as-is" (clone + read) and "fork for your team" (clone + customize org/ + add domain)
8. **How Roles Work**: Code-block example showing a multi-role task execution with role labels (like the `agent task --jira ENG-123` example)
9. **Portability table**: 4 environments (cloud, on-prem, hybrid, air-gapped) — works? notes
10. **License**: MIT, one line
11. **Contributing**: 5 bullet points for contribution types (roles, domains, tools, framework, workflows)

### `DIRECTORY_GUIDE.md` — File-by-File Reference

For EVERY file and directory in the project, provide:

```markdown
### `path/to/file`

**Purpose:** [1-2 sentences: why it exists]

**How to use:** [2-4 bullet points: what to do with it]

**When to modify:** [1 sentence: what triggers an update]
```

Organize by directory. Cover:

- **Root files**: README.md, LICENSE, PLAN.md, CUSTOMIZATION.md, DIRECTORY_GUIDE.md, .gitignore
- **roles/**: README.md + all 9 role files including customer-persona.md (explain what each role definition contains)
- **domains/**: README.md + domains/relevancy/ (all 5 files)
- **org/**: profile.md, infrastructure.md, policies.md
- **plan/**: All 6 plan files + all 7 phase files
- **tools/**: All 4 tool directories (README + workflows per tool)
- **agent-core/**: All subdirectories (cli, integrations/jira, integrations/confluence, integrations/git, evaluations, data-analysis, app-builder)
- **docs/**: guides/, architecture/
- **templates/**: All template files
- **config/**: Purpose and security note
- **prompts/**: Purpose and how to use

End with a **summary table**: "I'm doing X → touch these files" (12+ rows covering: adopting for org, adding domain, adding/modifying role, planning, building, setting up tools, evaluations, documentation, architecture decisions, integrations, onboarding, reviewing behavior)

### `CUSTOMIZATION.md` — Adoption Guide

Structure:

1. **Introduction**: This is a structural template. Fork, extend, customize. Roles are universal, domains are specific.

2. **How to Adopt (7 steps)**:
   - Step 1: Fork the repo
   - Step 2: Fill out org/profile.md
   - Step 3: Fill out org/infrastructure.md
   - Step 4: Configure roles (keep all 9, prioritize subset, or add new ones)
   - Step 5: Add your domain (with `cp` commands copying from reference domain)
   - Step 6: Add policies and guardrails
   - Step 7: Create CLAUDE.md

3. **Extension Points**: Table listing all documents with "Organization Extension Point" markers

4. **Adding Your Domain**: Domain skill template showing the 8-stage structure to fill in. Table of 7+ example domains with key differences from the reference domain.

5. **Policies, Standards, and Guardrails**:
   - Complete policy template (duplicated from org/policies.md for reference)
   - Enforcement mechanisms table (8 mechanisms: branch protection, CI gates, MCP permissions, API scopes, hooks, CLAUDE.md, eval gates, audit logging)

6. **Scaling Across Teams**:
   - Single team: one repo structure
   - Multiple teams: shared framework + team forks structure
   - Organization-wide: central governance + team configs structure

7. **Configuration as Code**: Table showing every configuration type, location, format, and reviewability (10+ rows, including roles and domains)

8. **Getting Started Checklist**: 11 checkbox items covering the full adoption process

## Quality Criteria

- README must be scannable in under 2 minutes (use tables, not paragraphs)
- DIRECTORY_GUIDE must cover every single file (no gaps)
- CUSTOMIZATION must be step-by-step actionable (not just descriptive)
- All three documents must reference each other for navigation
- The multi-role task execution example in README must show 4+ roles with realistic output

## Verification

- 3 files exist at project root
- README has the 9-role table and directory tree
- DIRECTORY_GUIDE covers every file and directory in the project
- CUSTOMIZATION has the 7-step adoption process and scaling patterns
- All checkbox lists are actionable
- Commit with message: "Add README, directory guide, and customization documentation"
