# Prompt 02: Generate Role Definitions

## Context

You are building a multi-role software engineering agent framework. The directory structure exists (from Prompt 01). Now you need to create the role definitions — the core of what makes this a multi-role agent.

The agent plays 9 roles. Each role is a distinct perspective with specific skills, decision frameworks, and outputs. The agent switches roles based on the task, and often combines multiple roles on a single task.

## Objective

Create `roles/README.md` and 9 role definition files in `roles/`.

## Instructions

### `roles/README.md` — Role System Overview

Write a README that explains:

1. **How roles work**: The agent determines which role(s) to activate based on the task
2. **Role selection**: Show 3 examples of task → role mapping (including multi-role)
3. **Role switching**: The agent explicitly states which role it's operating in and why
4. **Role combinations**: Table mapping common task types to role sequences (at least 8 rows)
5. **Role index**: Table listing all 9 roles with file link and one-line summary
6. **Adding a new role**: Step-by-step instructions

### Role Definition Files

Create one file per role. Each file MUST follow this exact structure:

```markdown
# Role: [Name]

## Identity
[2-3 sentences: what this role does and its core purpose]
[When the agent activates this role: list of trigger scenarios]

## Perspective
[5 questions this role asks when approaching any problem — "The X asks:"]
[5 things this role avoids — "The X avoids:"]

## Core Skills
[3-6 skill categories, each with a table or detailed list]
[Include concrete techniques, patterns, or frameworks — not vague descriptions]

## Decision Framework
[Numbered steps this role follows when making decisions]
[This should be specific enough that someone could follow it mechanically]

## Inputs and Outputs
[What this role consumes (from other roles)]
[What this role produces (for other roles and for the team)]

## How the Agent Performs This Role
[Concrete example showing the agent executing this role on a real task]
[Use code-block format showing the command and step-by-step agent behavior]
```

### The 9 Roles

**1. Architect** (`architect.md`)
- Skills: system design, technology evaluation, tradeoff analysis (table with dimensions like consistency vs. availability, latency vs. throughput, etc.), architecture patterns (list 8+), non-functional requirements
- Decision framework: clarify requirements → identify options → evaluate tradeoffs → recommend → document

**2. Developer** (`developer.md`)
- Skills: code generation, code modification, debugging, full-stack competence (table by layer: frontend, backend, data, infrastructure, build), code quality
- Decision framework: understand → plan → implement → test → review → commit

**3. Tester** (`tester.md`)
- Skills: test strategy, test pyramid (diagram + table by level), edge case thinking (comprehensive table with 8+ categories: boundary, null, concurrency, state, scale, encoding, time, network), test automation
- Decision framework: understand change → identify risks → choose test levels → write tests → run → report

**4. UX Expert** (`ux-expert.md`)
- Skills: user research, interaction design, design principles (table with 6 principles: clarity, consistency, feedback, forgiveness, efficiency, accessibility), information architecture, design systems
- Decision framework: understand user → map flow → design interaction → consider edges → validate accessibility → iterate

**5. Product Manager** (`product-manager.md`)
- Skills: problem definition, requirements/stories (INVEST checklist table), prioritization frameworks (table with 6+: RICE, ICE, value/effort, opportunity scoring, Kano, weighted scoring), metrics, stakeholder management
- Decision framework: identify problem → explore solutions → define scope → write requirements → prioritize → communicate

**6. Project Manager** (`project-manager.md`)
- Skills: planning, tracking (table: what to track, how, why — 6 items), risk management (identify → assess → mitigate → monitor → escalate), communication, scope management
- Decision framework: plan → track → surface → decide → communicate → retrospect

**7. Program Manager** (`program-manager.md`)
- Skills: cross-team coordination, roadmap management, dependency management (table by type: technical, data, resource, knowledge, external), stakeholder communication, portfolio prioritization
- Decision framework: align → map → track → coordinate → escalate → report

**8. Data Scientist** (`data-scientist.md`)
- Skills: data analysis, ML (table by category: supervised, unsupervised, NLP, ranking, recommendation, evaluation), experimentation (design → execute → analyze → interpret), data engineering, visualization
- Decision framework: frame → explore → analyze → validate → communicate → recommend

**9. Customer Persona** (`customer-persona.md`)
- Skills: 5 persona dimensions tables (relationship, technical sophistication, demographics, behavioral patterns, emotional state), reaction prediction table (8+ stimulus types), journey simulation methodology, empathy calibration, feedback translation, 3 worked examples (search results, error message, feature proposal), pre-defined persona YAML template, anti-patterns table (6+)
- Decision framework: identify persona → simulate reaction → predict behavior → validate assumptions → translate feedback → recommend changes

## Quality Criteria

- Each role file should be 80-120 lines of markdown
- Skills must include concrete techniques, not just category names
- Tables should have 4+ rows with specific, actionable content
- Examples should use realistic engineering scenarios
- Perspectives should be distinctive — reading any role file should feel like a different person is thinking
- The "avoids" section should include real anti-patterns, not generic warnings

## Verification

- All 10 files exist in `roles/`
- Each role file follows the exact structure (Identity, Perspective, Core Skills, Decision Framework, Inputs/Outputs, How the Agent Performs)
- `roles/README.md` includes role combination table with 8+ task types
- No two roles have the same perspective or decision framework
- Commit with message: "Add 9 role definitions with switching and combination logic"
