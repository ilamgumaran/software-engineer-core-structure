# AGENTS

**HIO-Based Engineering Org Setup** -- the structural template for setting up and running an engineering organization on HIO principles. Roles, goals, effectiveness measures, transformation plan.

## Family

This repo is part of the HIO repo family. The central multi-repo spec is at [`software-engineering-hio-agent-framework/multi-repo-orchestration/`](https://github.com/ilamgumaran/software-engineering-hio-agent-framework/tree/main/multi-repo-orchestration).

| Repo | Relationship |
|---|---|
| [`thought-org-with-human-ai-hybrid`](https://github.com/ilamgumaran/thought-org-with-human-ai-hybrid) | Upstream -- the HIO methodology this repo applies |
| [`thoughtexperiments`](https://github.com/ilamgumaran/thoughtexperiments) | Two layers upstream -- Resonant Cognition Framework, the cognition foundation HIO rests on |
| [`software-engineering-hio-agent-framework`](https://github.com/ilamgumaran/software-engineering-hio-agent-framework) | Downstream -- the day-to-day agentic toolkit used inside an HIO-aligned engg org; multi-repo spec hosted there |

## Purpose and scope

This repo is the structural template for **setting up and running an engineering organization on HIO principles**. It owns the role taxonomy, the goals and effectiveness measures, and the transformation plan from a non-HIO state to an HIO-aligned state. It is HIO-coupled by design.

**In scope:** 9 role definitions, domain extension system, transformation phase plans, goals templates, effectiveness measures, foundational skills and tools, infrastructure and policy templates, regeneration prompts.

**Out of scope:** HIO methodology principles (those live upstream in `thought-org-with-human-ai-hybrid`), day-to-day agent operation (that lives downstream in `software-engineering-hio-agent-framework`), forks' instantiated org configuration (lives in forks).

## Key concepts owned here

- The 9 roles used when setting up an HIO-aligned engineering org: Architect, Developer, Tester, UX Expert, Product Manager, Project Manager, Program Manager, Data Scientist, Customer Persona
- Domain extension system (`domains/<name>/`)
- Org-level goals and effectiveness measures, mapped to the 4 HIO Core Principles
- The 7-phase transformation plan from non-HIO to HIO-aligned
- The customization workflow (fork, fill `org/`, add domain, configure agent)
- Foundational skills and the foundational tools stack at the org level

## How to make changes

- Branch from `main` using a descriptive feature branch name
- Keep the 9 roles stable; renames require deprecation per upstream HIO governance
- Use the relevancy domain as the example for new patterns
- Keep `org/` template entries un-instantiated -- the templates are filled by forks
- Cross-link upstream to `thought-org-with-human-ai-hybrid` for HIO principles, and downstream to `software-engineering-hio-agent-framework` for day-to-day agent operations
- Markdown only, no YAML frontmatter, tables with 3+ rows

## Dos and don'ts

**Do:**
- Anchor every addition to one of the 4 HIO Core Principles or one of the 9 roles
- Keep this repo focused on **org setup, goals, measures, transformation** -- day-to-day agent operation belongs downstream
- Cite upstream HIO methodology when introducing concepts; do not redefine
- Update `CUSTOMIZATION.md` when adding extension points

**Don't:**
- Rename or remove a role without a deprecation period in `PLAN.md`
- Treat HIO as optional -- this repo is the HIO-applied engineering-org template; HIO coupling is the point
- Pre-commit a filled `org/profile.md`
- Add day-to-day agent operation content here -- those belong in `software-engineering-hio-agent-framework`

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
| Modify goals or effectiveness measures | Interactive | Affects how forks measure HIO alignment |
| Modify transformation phases | Interactive | Practitioners depend on this for org change |

Full table: [central matrix](https://github.com/ilamgumaran/software-engineering-hio-agent-framework/blob/main/multi-repo-orchestration/hio-collaboration/matrix.md).

## Security boundaries

**An agent may:**
- Read and modify framework documents in feature branches
- Add example content to the relevancy domain
- Open PRs and comment on issues

**An agent must not:**
- Rename or remove the 9 roles
- Modify the 4 HIO Core Principles (those are upstream)
- Push to `main`
- Pre-fill `org/` templates with concrete data
- Move day-to-day agent operation content here

For org-wide rules, see [security-and-safety](https://github.com/ilamgumaran/software-engineering-hio-agent-framework/blob/main/multi-repo-orchestration/governance/security-and-safety.md).

## Trace links

| Need | Look at |
|---|---|
| HIO methodology and principles | [`thought-org-with-human-ai-hybrid`](https://github.com/ilamgumaran/thought-org-with-human-ai-hybrid) |
| Cognition foundation (two layers upstream) | [`thoughtexperiments`](https://github.com/ilamgumaran/thoughtexperiments) |
| Day-to-day agentic toolkit (downstream) | [`software-engineering-hio-agent-framework`](https://github.com/ilamgumaran/software-engineering-hio-agent-framework) |
| Multi-repo orchestration -- registry, spec, scoring | [`multi-repo-orchestration/`](https://github.com/ilamgumaran/software-engineering-hio-agent-framework/tree/main/multi-repo-orchestration) |
| 9 role definitions | [`roles/`](roles/) |
| Reference domain (relevancy engineering) | [`domains/relevancy/`](domains/relevancy/) |
| Transformation plan | [`PLAN.md`](PLAN.md) |
| Customization for forks | [`CUSTOMIZATION.md`](CUSTOMIZATION.md) |

## Spec version

Spec: AGENTS-SPEC-v1
