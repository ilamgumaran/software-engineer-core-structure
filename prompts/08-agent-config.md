# Prompt 08: Generate Agent Configuration Guide

## Context

You are building a multi-role software engineering agent framework. All the structural components exist (roles, domains, plan, tools, org config, templates). Now you need the guide for creating the actual CLAUDE.md (or equivalent) that configures the AI agent to use all of this.

## Objective

Create `docs/guides/agent-configuration.md` — a comprehensive guide for creating the CLAUDE.md file that ties everything together.

## Instructions

### `docs/guides/agent-configuration.md`

Write a guide with these sections:

**1. What Is CLAUDE.md**
- Explain that CLAUDE.md is the persistent project context file that the AI reads on every invocation
- It's the "operating manual" for the agent — defines who it is, what it knows, how it should behave
- For this framework, CLAUDE.md must include role definitions (all 9 roles including Customer Persona), domain knowledge, and organizational context

**2. CLAUDE.md Structure**

Provide the complete recommended structure:

```markdown
# Project: [Name]

## Agent Identity
You are a multi-role software engineering agent. You operate as 9 roles:
[list roles with one-line descriptions, including Customer Persona]

## Role Activation
When given a task:
1. Identify which role(s) are needed
2. State which role you're activating and why
3. Execute with that role's perspective and decision framework
4. Switch roles when the task requires a different perspective

Role definitions are in roles/*.md — read them for detailed guidance.

## Domain
Your domain expertise is in [domain name].
Domain knowledge is in domains/[domain]/ — read these files for subject-matter expertise.

## Project Overview
[Description of what this project/codebase does]

## Directory Structure
[Key directories and what they contain]

## Conventions
[Coding style, language versions, formatting tools, naming conventions]

## Git Conventions
[Branch naming, commit message format, PR description template]

## How to Run
[Commands for tests, lint, build, deploy, evaluation]

## Key Integrations
[Issue tracker, documentation platform, data sources — with env var references]

## Guardrails
[Reference org/policies.md — summarize the key CAN/CANNOT rules]
```

**3. Role Integration Patterns**

Show 3 examples of how the CLAUDE.md role section translates into agent behavior:

Example 1: Single-role task
- Input: "Fix the login timeout bug"
- CLAUDE.md guidance: Activate Developer role
- Agent behavior: Reads code → diagnoses → fixes → tests → commits

Example 2: Multi-role task
- Input: "Design and build a notification system"
- CLAUDE.md guidance: Sequence PM → Architect → Developer → Tester
- Agent behavior: Requirements → design → implement → validate

Example 3: Explicit role override
- Input: `agent --role data-scientist "Analyze conversion trends"`
- CLAUDE.md guidance: Override auto-selection, use Data Scientist
- Agent behavior: Query data → analyze → statistical tests → report

Example 4: Customer Persona validation
- Input: "Evaluate the new search results page from a customer perspective"
- CLAUDE.md guidance: Activate Customer Persona role, optionally combine with UX Expert
- Agent behavior: Select persona dimensions → simulate reaction → predict behavior → identify pain points → translate feedback → recommend changes

**4. MCP Server Configuration**

Show the complete `settings.json` structure for configuring MCP servers:

```json
{
  "mcpServers": {
    "issues": { ... },
    "docs": { ... },
    "data": { ... },
    "search": { ... }
  }
}
```

Include 4 MCP server examples with environment variable references.

**5. Memory Seeding**

List 10+ memory commands to seed the agent with project knowledge:
- Team structure memories
- Domain baseline memories
- Convention/process memories
- Integration configuration memories

**6. Hooks Configuration**

Show 3 hook examples:
- Post-commit: remind about issue linking
- Post-task: trigger documentation update
- Pre-push: validate branch naming

**7. Customization Checklist**

A checkbox list for completing CLAUDE.md configuration:
- [ ] Agent identity and role system defined
- [ ] Domain referenced
- [ ] Project overview and structure documented
- [ ] Conventions (code, git, docs) specified
- [ ] Run commands listed
- [ ] Integration credentials configured (env vars)
- [ ] Guardrails from org/policies.md summarized
- [ ] MCP servers configured in settings.json
- [ ] Memory seeded with key project facts
- [ ] Hooks configured for workflow automation
- [ ] Tested: agent responds correctly to role-switching commands

## Quality Criteria

- The CLAUDE.md template must be copy-paste-able (fill in brackets and it works)
- MCP server configs must use environment variable references (never hardcode secrets)
- Memory seeding examples must be specific and realistic
- The guide should be readable by someone who has never used Claude Code

## Verification

- File exists at `docs/guides/agent-configuration.md`
- Contains complete CLAUDE.md template
- Contains 4 MCP server configuration examples
- Contains 10+ memory seeding commands
- Contains customization checklist
- Commit with message: "Add agent configuration guide with CLAUDE.md template"
