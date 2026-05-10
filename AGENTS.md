# AGENTS

The generic, forkable Multi-Role Software Engineering Agent Framework. Domain-agnostic predecessor to the HIO operational hub.

## Family

This repo is part of the HIO repo family. The central spec is at [`software-engineering-hio-agent-framework/multi-repo-orchestration/`](https://github.com/ilamgumaran/software-engineering-hio-agent-framework/tree/main/multi-repo-orchestration).

| Repo | Relationship |
|---|---|
| [`software-engineering-hio-agent-framework`](https://github.com/ilamgumaran/software-engineering-hio-agent-framework) | Downstream HIO superset that extends this framework |
| [`thought-org-with-human-ai-hybrid`](https://github.com/ilamgumaran/thought-org-with-human-ai-hybrid) | Sibling -- HIO methodology that informs the downstream extension |
| [`thoughtexperiments`](https://github.com/ilamgumaran/thoughtexperiments) | Sibling in the family; no direct dependency |

## Purpose and scope

This repo is the structural template for building an AI agent that operates across 9 engineering roles. It is intentionally domain-agnostic; the relevancy domain is the reference implementation, but the framework applies to any engineering team.

**In scope:** 9 role definitions, domain extension system, 7-phase implementation plan, foundational skills and tools, infrastructure and policy templates, regeneration prompts.

**Out of scope:** HIO-specific concepts (those live in the operational hub), specific runtime code (planned in `agent-core/`), forks' instantiated configuration (lives in forks).

## Key concepts owned here

- The 9 roles: Architect, Developer, Tester, UX Expert, Product Manager, Project Manager, Program Manager, Data Scientist, Customer Persona
- Domain extension system (`domains/<name>/`)
- The 7-phase implementation plan (CLI, Developer+Tester, Integrations, Architect+DS, PM+UX, Domain+Docs, UI)
- The customization workflow (fork, fill `org/`, add domain, configure agent)
- Foundational skills and the foundational tools stack

## How to make changes

- Branch from `main` using a descriptive feature branch name
- Keep the 9 roles stable; renames require deprecation
- Use the relevancy domain as the example for new patterns
- Keep `org/` template entries un-instantiated -- the templates are filled by forks
- Markdown only, no YAML frontmatter, tables with 3+ rows

## Dos and don'ts

**Do:**
- Keep the 9 roles stable
- Use the relevancy domain for example additions
- Update `CUSTOMIZATION.md` when adding extension points
- Keep this repo HIO-agnostic; HIO is downstream, not upstream

**Don't:**
- Rename or remove a role without a deprecation period in `PLAN.md`
- Couple this repo to HIO concepts (cognitive functions, agent types)
- Pre-commit a filled `org/profile.md`
- Add CI that requires HIO-specific structures

Full list: [`per-repo-software-engineer-core-structure.md`](https://github.com/ilamgumaran/software-engineering-hio-agent-framework/blob/main/multi-repo-orchestration/dos-and-donts/per-repo-software-engineer-core-structure.md).

## HIO routing

| Task signal | Route | Why |
|---|---|---|
| Typo fix in non-canonical doc | II | Reversible, mechanical |
| Edit `roles/` role definitions | Interactive | Forks depend on stable definitions |
| Rename a role | OI | Cascade to all forks |
| Edit `CUSTOMIZATION.md` policies template | Interactive | Forks instantiate this template |
| Edit `domains/relevancy/` content | II | Reversible, illustrative |
| Add a 10th role | OI | Identity-level for the framework |
| Edit regeneration prompts (substantive) | Interactive | Affects forks that regenerate |

Full table: [central matrix](https://github.com/ilamgumaran/software-engineering-hio-agent-framework/blob/main/multi-repo-orchestration/hio-collaboration/matrix.md).

## Security boundaries

**An agent may:**
- Read and modify framework documents in feature branches
- Add example content to the relevancy domain
- Open PRs and comment on issues

**An agent must not:**
- Rename or remove the 9 roles
- Push to `main`
- Pre-fill `org/` templates with concrete data
- Add HIO-specific structure or vocabulary

For org-wide rules, see [security-and-safety](https://github.com/ilamgumaran/software-engineering-hio-agent-framework/blob/main/multi-repo-orchestration/governance/security-and-safety.md).

## Trace links

| Need | Look at |
|---|---|
| HIO superset that extends this framework | [`software-engineering-hio-agent-framework`](https://github.com/ilamgumaran/software-engineering-hio-agent-framework) |
| HIO methodology and principles | [`thought-org-with-human-ai-hybrid`](https://github.com/ilamgumaran/thought-org-with-human-ai-hybrid) |
| Multi-repo orchestration -- registry, spec, scoring | [`multi-repo-orchestration/`](https://github.com/ilamgumaran/software-engineering-hio-agent-framework/tree/main/multi-repo-orchestration) |
| 9 role definitions | [`roles/`](roles/) |
| Reference domain (relevancy engineering) | [`domains/relevancy/`](domains/relevancy/) |
| Implementation plan | [`PLAN.md`](PLAN.md) |
| Customization for forks | [`CUSTOMIZATION.md`](CUSTOMIZATION.md) |

## Spec version

Spec: AGENTS-SPEC-v1
