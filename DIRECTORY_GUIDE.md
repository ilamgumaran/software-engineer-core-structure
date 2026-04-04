# Directory and File Guide

A complete reference for every file and directory in this repository — what it is, why it exists, and how to use it.

---

## Root Files

### `README.md`

**Purpose:** The front door of the repository. Provides the 30-second overview for anyone landing here for the first time — what this project is, who it's for, what's inside, and how to get started.

**How to use:**
- Read this first when you encounter the repo
- Share this link when introducing the project to someone
- When forking for your org, update the title, description, and Quick Start section to reflect your team

**When to modify:** When you add new top-level files, directories, or significantly change the project scope.

---

### `PLAN.md`

**Purpose:** The executive summary of the entire plan. A single page that a team lead or manager can read in 5 minutes to understand the phased approach, timeline, and success criteria without diving into details.

**How to use:**
- Read this to get the full picture before diving into any phase
- Use as the agenda document in planning meetings
- Reference when someone asks "what are we building and when?"
- Update the phase timeline as actual progress diverges from estimates

**When to modify:** When phases are added, removed, reordered, or re-scoped. When success criteria change.

---

### `CUSTOMIZATION.md`

**Purpose:** The adoption guide for organizations forking this framework. Explains step-by-step how to take this generic framework and make it yours — replacing the domain, plugging in your infrastructure, and defining your guardrails.

**How to use:**
- Read this when you decide to adopt the framework for your team
- Follow the 6-step adoption process in order
- Use the domain skill template when replacing relevancy engineering with your domain
- Reference the scaling patterns section when expanding from one team to multiple teams

**When to modify:** When you discover new extension points or adoption patterns. When new domains are added as examples.

---

### `LICENSE`

**Purpose:** MIT License. Grants unrestricted permission to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of this software. No conditions except including the license text.

**How to use:**
- You don't need to do anything — the license applies automatically
- If you fork and redistribute, keep this file in your fork
- If you build a commercial product on top of this, that's allowed — no attribution required beyond keeping the license file

**When to modify:** Never modify the license text. You may update the copyright line if your organization requires it.

---

### `.gitignore`

**Purpose:** Tells git which files and directories to exclude from version control — preventing accidental commits of secrets, build artifacts, IDE files, and OS-generated files.

**How to use:**
- It works automatically — git reads it on every operation
- If a new file type should be excluded (e.g., your team uses a specific IDE), add a pattern here

**What it excludes:**
- Python: `__pycache__/`, `*.egg-info/`, `dist/`, `.venv/`
- IDE: `.idea/`, `.vscode/`, `*.swp`
- Environment: `.env`, `*.credentials.json`
- State: `*.db`, `.relevancy-agent/`
- OS: `.DS_Store`, `Thumbs.db`
- Node: `node_modules/`, `.next/`

**When to modify:** When you add new languages, tools, or frameworks that produce artifacts that shouldn't be committed.

---

### `DIRECTORY_GUIDE.md`

**Purpose:** This file. A complete reference explaining the purpose and usage of every file and directory.

**How to use:**
- Read when you're unsure what a file or directory is for
- Reference when onboarding new team members
- Update when adding new files or directories

---

## `roles/` — Agent Role Definitions

**Purpose:** Defines the 9 roles the agent can play. Each role file specifies the role's identity, perspective, core skills, decision framework, inputs/outputs, and how the agent performs that role. The roles README explains how role switching works.

**How to use as a directory:**
- Read `roles/README.md` first to understand how role selection and switching works
- Read individual role files when you want to understand a specific role's capabilities
- When the agent activates a role, it follows the perspective and decision framework defined here
- To add a new role, create a new `.md` file following the existing template structure

---

### `roles/README.md`

**Purpose:** Explains the role system — how the agent selects roles, switches between them, and combines multiple roles on a single task. Includes a role combination matrix showing which roles activate for common task types.

**How to use:** Read this to understand the multi-role orchestration. Reference the role combination table when designing new workflows.

---

### `roles/architect.md`

**Purpose:** Defines the Architect role — system design, technology evaluation, tradeoff analysis, architecture patterns, non-functional requirements. Includes the decision framework (clarify → identify options → evaluate → recommend → document).

**How to use:** The agent reads this when activated as Architect. Engineers can read it to understand what to expect from the agent in this role.

---

### `roles/developer.md`

**Purpose:** Defines the Developer role — code generation, modification, debugging, full-stack competence, code quality. The most frequently activated role.

**How to use:** The agent reads this when writing or modifying code. The decision framework (understand → plan → implement → test → review → commit) guides every code change.

---

### `roles/tester.md`

**Purpose:** Defines the Tester role — test strategy, test pyramid, edge case thinking, test automation. Includes comprehensive edge case categories (boundary values, null/missing, concurrency, encoding, time).

**How to use:** The agent reads this when writing tests or validating changes. The edge case table is especially valuable — it ensures the agent thinks adversarially.

---

### `roles/ux-expert.md`

**Purpose:** Defines the UX Expert role — user research, interaction design, design principles, information architecture, design systems. Includes the 6 core design principles (clarity, consistency, feedback, forgiveness, efficiency, accessibility).

**How to use:** The agent reads this when reviewing UI, auditing accessibility, or designing user flows.

---

### `roles/product-manager.md`

**Purpose:** Defines the Product Manager role — problem definition, requirements writing, prioritization frameworks (RICE, ICE, MoSCoW, Kano), metrics, stakeholder management.

**How to use:** The agent reads this when scoping features, writing user stories, or prioritizing backlog.

---

### `roles/project-manager.md`

**Purpose:** Defines the Project Manager role — planning, tracking, risk management, communication, scope management. Includes what to track (velocity, blockers, risks, scope, dependencies).

**How to use:** The agent reads this when planning sprints, generating status reports, or managing risks.

---

### `roles/program-manager.md`

**Purpose:** Defines the Program Manager role — cross-team coordination, roadmap management, dependency tracking, stakeholder communication, portfolio prioritization.

**How to use:** The agent reads this when coordinating across teams, aggregating status, or escalating decisions.

---

### `roles/data-scientist.md`

**Purpose:** Defines the Data Scientist role — data analysis, ML techniques, experimentation, data engineering, visualization. Includes the ML technique taxonomy and experimentation methodology.

**How to use:** The agent reads this when analyzing data, designing experiments, or building models.

---

### `roles/customer-persona.md`

**Purpose:** Defines the Customer Persona role — how the agent simulates specific customer types to predict reactions, validate UX decisions, and identify friction points from the user's perspective.

**How to use:**
- Read when evaluating features, UX changes, error messages, or search results from the customer's point of view
- Reference persona dimensions (relationship type, technical sophistication, demographics, behavior, emotional state) when constructing specific personas
- Use pre-defined persona templates or construct personas on the fly
- Feed outputs (friction maps, drop-off predictions, reaction assessments) into Product Manager and UX Expert workflows

**When to modify:** When adding new persona dimensions, updating persona templates, or refining how the agent simulates customer behavior.

---

## `domains/` — Domain-Specific Knowledge

**Purpose:** Contains subject-matter expertise that supplements the role definitions. Roles define *how* the agent thinks; domains define *what* it knows about your specific problem space. Domains are the primary extension point for customizing the agent to your team's work.

**How to use as a directory:**
- The `relevancy/` subdirectory is a fully worked reference example
- To add your domain, create `domains/<your-domain>/` with the standard files (overview, skills, evaluation, workflows, glossary)
- The agent loads domain knowledge alongside role definitions

---

### `domains/README.md`

**Purpose:** Explains how domains work, what files each domain needs, lists example domains, and provides step-by-step instructions for adding a new domain.

**How to use:** Read this before adding a new domain. Use it as a checklist for what files to create.

---

### `domains/relevancy/`

**Purpose:** The reference domain implementation — relevancy engineering. Contains complete domain knowledge: search pipeline concepts, ranking algorithms, evaluation metrics, domain workflows, and terminology.

**How to use:** Use this as a template when creating your own domain. If your team does relevancy engineering, use it as-is. Each file demonstrates the level of detail needed for effective domain configuration.

**Files:**
- `overview.md` — What relevancy engineering is, key concepts, why it matters
- `skills.md` — Domain-specific skills (search pipeline, ranking algorithms, evaluation)
- `evaluation.md` — How to measure quality (NDCG, MRR, A/B testing)
- `workflows.md` — Domain-specific multi-role workflow recipes
- `glossary.md` — Term definitions for the domain

---

## `org/` — Organization Configuration

**Purpose:** The place where an adopting organization defines who they are, what tools they use, and what rules the agent must follow. These files are templates — fill them in when you fork the repo.

**How to use as a directory:**
- This is the first directory to customize when adopting the framework
- The agent reads these files to understand your organization's context
- Treat changes to these files like configuration changes — they go through PR review

---

### `org/profile.md`

**Purpose:** Defines your team's identity — name, domain, size, roles, mission, customers, key systems, success metrics, and constraints. This is the "who are we" file that helps the agent tailor its behavior to your specific team.

**How to use:**
- Fill in every section when adopting the framework
- The agent reads this to understand who it's working for and what matters
- If your team's mission or structure changes, update this file
- Example: If you're a 5-person ML platform team, the agent should behave differently than if you're a 50-person backend engineering org

**When to modify:** When team structure changes, new systems are added, success metrics shift, or constraints are added/removed.

---

### `org/infrastructure.md`

**Purpose:** The technical decision record — what tools and platforms your organization uses at every layer of the stack. Source control platform, branching strategy, CI/CD system, deployment target, observability stack, data warehouse, and approved AI tools.

**How to use:**
- Fill in every section when adopting the framework
- The agent uses this to generate correct CI configs, deployment manifests, and integration code
- When evaluating a new tool, update the relevant section and note the migration plan
- This file answers "what do we use for X?" definitively

**When to modify:** When you adopt a new tool, change platforms, or add new infrastructure components. Treat this as a living document — review quarterly.

---

### `org/policies.md`

**Purpose:** The guardrails and boundaries for the AI agent — what it can access, what it cannot touch, what quality gates must pass, and when it must escalate to a human. This is the "rules of engagement" file.

**How to use:**
- Fill in every section when adopting the framework
- Check the boxes that apply to your organization (they're all unchecked by default)
- Add organization-specific policies not covered by the template
- The agent reads this to know its boundaries — a well-defined policy file prevents the agent from overstepping
- Enforcement mechanisms (branch protection, MCP permissions, CI gates) should match what's declared here

**When to modify:** When policies change, new compliance requirements appear, or incidents reveal gaps in the guardrails. After any security incident involving the agent, review and tighten this file.

---

## `plan/` — Planning Documents

**Purpose:** The detailed brain of the project. Contains the vision, capabilities, architecture, implementation steps, required skills, and toolchain — everything needed to understand what we're building and how.

**How to use as a directory:**
- Files are numbered `00-` through `05-` for reading order
- Read them in order when onboarding to the project
- Reference specific files when working on a particular aspect
- The `phases/` subdirectory breaks the plan into executable chunks

---

### `plan/00-overview.md`

**Purpose:** The "why" document. Defines the vision, problem statement, goals with measurable targets, constraints, stakeholders, and tool strategy. This is what you show to leadership to explain why this project exists.

**How to use:**
- Read first to understand the motivation and scope
- Reference the goals table when measuring progress
- Reference the constraints when making design decisions (e.g., "can the agent have prod access?" — check constraints)
- Use the stakeholder table to understand who cares about what

**When to modify:** When the vision evolves, new constraints emerge, or stakeholders change. Goals and targets should be updated based on actual measurements.

---

### `plan/01-capabilities.md`

**Purpose:** The complete inventory of what the agent can do, organized by domain (app building, data analysis, evaluation, workflow, Q&A). Includes the CLI command design and the dependency graph between capabilities.

**How to use:**
- Reference when answering "can the agent do X?"
- Use the capability tables to scope what's included vs. excluded
- Use the CLI command reference when implementing or using the CLI
- The dependency graph at the bottom shows which capabilities must be built first
- When forking for a new domain, replace these tables with your domain's capabilities

**When to modify:** When new capabilities are added, existing ones are removed, or the CLI interface changes.

---

### `plan/02-architecture.md`

**Purpose:** The system architecture — component diagram, data flow, technology stack choices, and security model. Explains how the pieces fit together and how a request flows from user input to completed task.

**How to use:**
- Reference when making implementation decisions ("where does this code go?")
- Use the component details to understand responsibilities and boundaries
- Use the data flow diagram to trace how a task moves through the system
- Use the technology stack table when setting up the development environment
- Use the security model when designing API tokens and access controls

**When to modify:** When architecture changes — new components, different tech stack choices, or changes to the security model. Create an ADR in `docs/architecture/` for significant changes.

---

### `plan/03-implementation-guide.md`

**Purpose:** The "how" document. Every step in the plan explained with: what to do, exact code/commands, how the AI tools help, expected outcome, and verification steps. This is the document you have open while building.

**How to use:**
- Follow steps in order within each phase (they have dependency chains)
- Each step has a "Verification" section — don't move to the next step until verification passes
- Code examples are starting points, not copy-paste solutions — adapt to your codebase
- The summary table at the bottom shows the full dependency graph across all steps
- When stuck on a step, the "How Claude Code helps" sections show exact prompts to use

**When to modify:** When implementation approach changes, new steps are discovered, or verification criteria need updating. Keep this in sync with actual implementation experience.

---

### `plan/04-foundational-skills.md`

**Purpose:** The domain knowledge document. Maps the 8-stage end-to-end problem-solving journey with the specific skills needed at each stage — from understanding a customer complaint to delivering a validated, documented fix. Includes a 4-level maturity model.

**How to use:**
- Read to understand what domain expertise the agent (and your team) needs
- Use the problem decomposition trees as diagnostic frameworks
- Use the metrics tables as reference when designing evaluations
- Use the maturity model to assess and track the agent's growth
- Use the skill development roadmap to prioritize what to build into the agent first
- When forking for a new domain, replace the 8 stages with your domain's problem-solving journey

**When to modify:** When new skills are identified, the maturity model levels are refined, or the domain focus shifts.

---

### `plan/05-foundational-tools.md`

**Purpose:** The infrastructure document. Maps the complete toolchain from Layer 0 (OS/hardware) through Layer 7 (AI tools) with every option at each layer, decision matrices, and portability considerations. Includes the bare-metal, container, VM, and serverless spectrum.

**How to use:**
- Reference when making infrastructure decisions
- Use the decision matrices to compare options at each layer
- Use the "Organization Extension Point" markers to know what to fill in for your org
- Use the portability matrix when planning multi-environment support
- Use the air-gapped stack section if your org can't use cloud services
- The Infrastructure Decision Record template at the bottom is the same template in `org/infrastructure.md`

**When to modify:** When new tools emerge, existing tools are deprecated, or the landscape shifts. This should stay current with the industry.

---

### `plan/phases/` — Phase Detail Documents

**Purpose:** Each phase broken down into specific deliverables, implementation steps with time estimates, and verification checklists. These are the sprint planning documents.

**How to use as a directory:**
- Pick the phase you're currently working on
- Use the deliverables list for sprint goals
- Use the implementation steps table for task breakdown
- Use the verification checklist as the "definition of done"

---

### `plan/phases/phase-1-cli-foundation.md`

**Purpose:** Phase 1 detail — building the CLI interface and configuring Claude Code as the execution engine. Covers CLAUDE.md creation, CLI application with typer, memory seeding, and MCP server configuration.

**How to use:** Follow the 9 implementation steps in order. Each step has a clear deliverable and verification. This is the foundation — nothing else works until Phase 1 is solid.

---

### `plan/phases/phase-2-integrations.md`

**Purpose:** Phase 2 detail — connecting to Jira, Confluence, and Git. Covers MCP server development, page templates, git workflow automation, and cross-referencing between systems.

**How to use:** Build the Jira MCP server first (Step 1-2), then Confluence (Step 3-4), then git automation (Step 5), then wire cross-references (Step 6). The end-to-end test (Step 7) validates everything works together.

---

### `plan/phases/phase-3-evaluation-engine.md`

**Purpose:** Phase 3 detail — the relevancy evaluation framework. Covers test suite format, evaluation runner, metrics calculator, configuration comparator, LLM-as-judge, and report generator.

**How to use:** Start with the test suite format (it defines the data contract), then build the runner, then metrics, then comparator. The report generator ties everything together. This is the most domain-specific phase.

---

### `plan/phases/phase-4-data-analysis.md`

**Purpose:** Phase 4 detail — customer behavior analysis. Covers data connectors, analysis library (CTR, funnels, trends), insight generator, and visualization.

**How to use:** Build data connectors first (must query your actual data warehouse), then implement analysis functions one at a time, starting with the most frequently asked questions on your team.

---

### `plan/phases/phase-5-documentation-automation.md`

**Purpose:** Phase 5 detail — automatic documentation generation. Covers auto-doc triggers, Confluence template system, documentation sync, and knowledge base building.

**How to use:** Build the template engine first, then add triggers to existing workflows (post-eval, post-merge). Documentation automation is highest value when it's invisible — things just get documented.

---

### `plan/phases/phase-6-ui-layer.md`

**Purpose:** Phase 6 detail — the web interface. Covers REST API, web app (Streamlit or React), core UI pages (task dashboard, conversation, evaluation viewer), and authentication.

**How to use:** Build the REST API first (it's a thin layer over the CLI). Start with Streamlit for fast iteration. Migrate to React+Next.js only if the tool becomes team-critical.

---

## `tools/` — AI Tool Guides

**Purpose:** Detailed capability guides and workflow recipes for each AI tool used in the framework. Each tool has a README (what it is, capabilities, setup, limitations) and a workflows file (concrete step-by-step recipes).

**How to use as a directory:**
- Read the README for a tool when deciding whether/how to use it
- Read the workflows file when you have a specific task and want to know the best approach
- When adding a new AI tool to your stack, create a new subdirectory following the same structure

---

### `tools/claude-code/README.md`

**Purpose:** The complete guide to Claude Code as the agent's execution engine. Covers CLAUDE.md, memory system, MCP servers, hooks, subagents, slash commands, setup steps, and limitations.

**How to use:**
- Read sections 1-6 to understand what Claude Code can do
- Follow the Setup Guide (Steps 1-6) when setting up for the first time
- Reference the MCP server configuration examples when adding integrations
- Reference the limitations section when the agent behaves unexpectedly

---

### `tools/claude-code/workflows.md`

**Purpose:** 8 concrete workflow recipes showing exactly how Claude Code executes common tasks — Jira story execution, evaluation runs, codebase Q&A, data analysis, documentation, onboarding, progress reports, and code review.

**How to use:**
- Find the workflow that matches your current task
- Each workflow shows the step-by-step flow Claude Code follows
- Use the Claude Code invocation examples as starting prompts
- Adapt workflows to your specific codebase and tools

---

### `tools/github-copilot/README.md`

**Purpose:** Guide to GitHub Copilot for in-IDE pair programming. Covers inline completion, Copilot Chat, PR assistance, CLI usage, and the key distinction from Claude Code (assists you vs. acts for you).

**How to use:**
- Read the "When to Use Copilot vs. Claude Code" table to understand the division of labor
- Follow the Setup Guide for IDE configuration
- Reference the effectiveness tips (descriptive function names, guiding comments)

---

### `tools/github-copilot/workflows.md`

**Purpose:** 5 workflow recipes for Copilot — writing evaluation test cases, implementing metrics, code review, SQL queries, and pair programming alongside the agent.

**How to use:** Find the workflow matching your in-IDE task. These are hands-on — you're typing and Copilot is assisting, unlike Claude Code workflows where the agent acts autonomously.

---

### `tools/gemini-enterprise/README.md`

**Purpose:** Guide to Gemini Enterprise for large-context analysis. Covers the 1M+ token context window, Google Workspace integration, LLM-as-judge at scale, and BigQuery integration.

**How to use:**
- Read the "When to Use Gemini vs. Claude Code" table to understand when Gemini is the better choice
- Follow the API Access section for programmatic integration
- Use for tasks that exceed Claude Code's context window or require bulk LLM operations

---

### `tools/gemini-enterprise/workflows.md`

**Purpose:** 4 workflow recipes for Gemini — bulk LLM-as-judge evaluation, large-scale data pattern detection, document corpus review, and cross-reference analysis.

**How to use:** These workflows are for bulk/large-scale tasks. Each shows how to batch work, structure prompts for consistency, and feed results back into the agent framework.

---

### `tools/glean/README.md`

**Purpose:** Guide to Glean for enterprise knowledge search. Covers cross-platform search, AI-powered answers, people/expertise discovery, API access, and Glean Chat.

**How to use:**
- Read the "When to Use Glean vs. Other Tools" table — Glean finds existing knowledge, other tools create new knowledge
- Follow the Setup Guide for API configuration and MCP server integration
- Use Glean when the agent needs context that spans multiple systems (Jira + Confluence + Slack + code)

---

### `tools/glean/workflows.md`

**Purpose:** 5 workflow recipes for Glean — context gathering before tasks, finding reviewers, answering "why" questions, onboarding support, and incident context.

**How to use:** These workflows show Glean as the first step before other tools act. Glean retrieves context, then Claude Code (or the engineer) acts on it.

---

## `agent-core/` — Agent Implementation

**Purpose:** Where the actual agent code will live. Currently contains empty directories that define the code organization. Code gets written here during implementation phases.

**How to use as a directory:**
- Don't add code here until you're in the implementation phase
- The directory structure maps to the architecture in `plan/02-architecture.md`
- Each subdirectory becomes a Python package/module

---

### `agent-core/cli/`

**Purpose:** The CLI interface layer — the `typer` application that team members interact with. Commands like `agent ask`, `agent task`, `agent eval`.

**How to use:** Implementation happens in Phase 1. This directory will contain `cli.py` (command definitions), and supporting modules for output formatting and input parsing.

**What goes here:** CLI command definitions, argument parsing, output formatting, interactive prompts. What does NOT go here: business logic, API calls, data processing — those go in other `agent-core/` directories.

---

### `agent-core/integrations/jira/`

**Purpose:** Jira API integration — the MCP server and supporting code that lets the agent read stories, update status, add comments, and create sub-tasks.

**How to use:** Implementation happens in Phase 2 (Step 2.1). This directory will contain the MCP server code and Jira API client wrapper.

**What goes here:** Jira API client, MCP server tool definitions, Jira data models, authentication handling. What does NOT go here: business logic that decides when to update Jira — that lives in the task router.

---

### `agent-core/integrations/confluence/`

**Purpose:** Confluence API integration — the MCP server for creating and updating documentation pages.

**How to use:** Implementation happens in Phase 2 (Step 2.2). Contains MCP server code and Confluence API client wrapper.

**What goes here:** Confluence API client, MCP server tool definitions, page creation/update logic, template rendering integration.

---

### `agent-core/integrations/git/`

**Purpose:** Git workflow automation — structured branching, commit messages, and PR creation following team conventions.

**How to use:** Implementation happens in Phase 2 (Step 2.3). Contains git operation wrappers and convention enforcement.

**What goes here:** Branch naming logic, commit message formatting, PR description generation, cross-reference linking. Note: Much of git automation is handled by Claude Code natively via CLAUDE.md conventions — this directory is for additional automation beyond what CLAUDE.md provides.

---

### `agent-core/evaluations/`

**Purpose:** The relevancy evaluation framework — test suite loading, evaluation execution, metrics calculation, comparison, and report generation.

**How to use:** Implementation happens in Phase 3. This is the most code-heavy directory and the core of the domain-specific agent capability.

**What goes here:** Test suite parser, evaluation runner, search client abstraction, metrics calculator (NDCG, MRR, P@K, R@K, MAP), configuration comparator, statistical significance tests, LLM-as-judge framework, report generator.

---

### `agent-core/data-analysis/`

**Purpose:** Customer behavior analysis — data connectors, analysis functions, insight generation, and visualization.

**How to use:** Implementation happens in Phase 4. Contains reusable analysis functions and data access abstractions.

**What goes here:** Data connector abstraction (BigQuery/Snowflake), parameterized SQL templates, analysis functions (CTR, funnels, trends), insight summarizer, chart/table generators.

---

### `agent-core/app-builder/`

**Purpose:** Application scaffolding and modification — the agent's ability to create new services, modify existing code, and manage project structure.

**How to use:** This capability is built incrementally across phases. Initially relies on Claude Code's native code generation; this directory adds domain-specific scaffolding templates and modification patterns.

**What goes here:** Project templates, code generation patterns specific to your domain, modification strategies for common change types.

---

## `docs/` — Documentation

**Purpose:** Team-facing documentation that helps people use the agent and understand the system. Separate from `plan/` (which is the build plan) — `docs/` is for users of the finished product.

---

### `docs/guides/`

**Purpose:** How-to guides for team members using the agent. "How do I run an evaluation?" "How do I ask the agent to analyze data?" "How do I onboard using the agent?"

**How to use:** Write guides here as features are completed. Each guide should be task-oriented (not concept-oriented) — start with what the reader wants to accomplish.

**What goes here:** User-facing how-to guides, quick-start documents, FAQ, troubleshooting guides.

---

### `docs/architecture/`

**Purpose:** Architecture Decision Records (ADRs) — the "why" behind significant technical decisions. When the team chooses Elasticsearch over Solr, or decides to use a two-stage ranking pipeline, the reasoning goes here.

**How to use:** Create a new ADR file whenever a significant architectural decision is made. Use the format: `NNNN-short-title.md` (e.g., `0001-use-elasticsearch.md`). Each ADR has: Context, Decision, Consequences.

**What goes here:** ADRs only. Not design docs (those go in Confluence), not implementation details (those go in code comments).

---

## `templates/` — Reusable Templates

**Purpose:** Jinja2 templates used by the agent to generate consistent, structured documents. The agent fills in variables and produces pages for Confluence, comments for Jira, and reports for evaluation results.

**How to use as a directory:**
- Templates use Jinja2 syntax (`{{ variable }}`, `{% for %}`, `{% if %}`)
- The agent's template engine loads these at runtime
- Modify templates to change the format of generated documents
- Add new templates when new document types are needed

---

### `templates/confluence/evaluation-report.md.j2`

**Purpose:** Template for evaluation reports published to Confluence. Includes sections for executive summary, configuration changes, metrics comparison table, regression analysis, improvement analysis, and recommendations.

**How to use:**
- The agent fills this template after running an evaluation with `--publish`
- Variables include: `config_name`, `baseline_name`, `date`, `metrics` (list), `regressions` (list), `improvements` (list), `recommendations`
- Modify the template to change report structure or add new sections
- The `{% for %}` loops handle variable-length data (metrics, regressions)

**When to modify:** When evaluation reports need new sections, different formatting, or additional data points.

---

### `templates/confluence/progress-update.md.j2`

**Purpose:** Template for periodic progress updates published to Confluence. Includes completed tasks, active work, key findings, metrics, and next steps.

**How to use:**
- The agent fills this template when running `agent report --publish`
- Variables include: `date_range`, `completed_tasks` (list), `active_tasks` (list), `findings` (list), `metrics` (list), `next_steps` (list)
- Each task object has `title`, `jira_id`, `summary`, `pr_url`, `confluence_url`

**When to modify:** When progress reports need different structure or additional context.

---

### `templates/evaluation-reports/`

**Purpose:** Directory for evaluation-specific report templates — different from Confluence templates. These produce standalone reports (markdown, HTML, or PDF) that can be viewed in the terminal or attached to PRs.

**How to use:** Add templates here for different report formats (terminal-friendly ASCII, PR-ready markdown, detailed HTML).

**Currently empty** — templates are added during Phase 3 implementation.

---

### `templates/jira/task-comment.md.j2`

**Purpose:** Template for structured comments the agent posts on Jira stories. Includes status, action summary, branch/PR/docs links, details, evaluation results, and next steps.

**How to use:**
- The agent fills this template when updating a Jira story after completing work
- Variables include: `status`, `action_summary`, `branch`, `pr_url`, `confluence_url`, `details`, `evaluation_summary`, `next_steps` (list)
- The template produces consistent, scannable Jira comments instead of freeform text

**When to modify:** When Jira comments need different structure or your team wants different information density.

---

## `config/` — Configuration Files

**Purpose:** Runtime configuration for the agent — data source connections, evaluation thresholds, tool settings, and environment-specific overrides.

**How to use:** Add configuration files here as the agent is implemented. Examples:
- `data-sources.yaml` — Database connections and credentials references
- `eval-thresholds.yaml` — Metric thresholds for pass/fail gates
- `agent-settings.yaml` — Agent behavior configuration

**Currently empty** — configuration files are added during implementation.

**Security note:** Never commit secrets or credentials to this directory. Use environment variable references (`${ENV_VAR}`) in config files and document required variables in `org/infrastructure.md`.

---

## `prompts/` — Framework Recreation Prompts

**Purpose:** Contains the structured prompts that can regenerate this entire framework from scratch. These are the "recipe" — feed them to an AI agent and it produces the framework.

**How to use as a directory:**
- Run `00-master.md` alone to generate everything in one shot
- Or run `01-` through `09-` individually in sequence for more control
- Modify prompts before running to customize the output (different roles, different domain, different tools)

---

### `prompts/README.md`

**Purpose:** Explains the prompt system — architecture, execution order, three usage options (master, individual, customize-first), and design principles.

---

### `prompts/00-master.md`

**Purpose:** The single all-in-one prompt. Contains complete instructions to generate every file in the framework from an empty directory. This is the most important file in `prompts/` — it's the framework as a prompt.

**How to use:** Feed this to an AI agent (Claude Code, or similar) in an empty git repo. It will generate 40+ files covering roles, domains, plans, tools, org templates, document templates, and documentation.

---

### `prompts/01-scaffold.md` through `prompts/09-documentation.md`

**Purpose:** Individual prompts that each generate one layer of the framework:

| Prompt | What It Generates |
|--------|------------------|
| `01-scaffold.md` | Directory structure, .gitignore, LICENSE |
| `02-roles.md` | 9 role definition files + roles README |
| `03-domains.md` | Domain system + reference domain (relevancy) |
| `04-plan.md` | PLAN.md + 6 plan documents + 7 phase files |
| `05-tools.md` | 4 tool guides (README + workflows each) |
| `06-org.md` | 3 org configuration templates |
| `07-templates.md` | 3 Jinja2 document templates |
| `08-agent-config.md` | Agent configuration guide with CLAUDE.md template |
| `09-documentation.md` | README, DIRECTORY_GUIDE, CUSTOMIZATION |

**How to use:** Run in numerical order. Each prompt is self-contained with full context.

**When to modify:** When you want to change what the framework generates — different roles, different domain, different tools, different organizational defaults.

---

## Summary: When Do I Touch What?

| I'm doing... | Touch these files/dirs |
|--------------|----------------------|
| **Adopting for my org** | `org/profile.md`, `org/infrastructure.md`, `org/policies.md` |
| **Adding my domain** | `domains/<name>/` (copy from `domains/relevancy/`) |
| **Adding or modifying a role** | `roles/<role>.md`, `roles/README.md` |
| **Planning the project** | `PLAN.md`, `plan/00-overview.md`, `plan/phases/` |
| **Building the agent** | `agent-core/`, `config/`, `plan/03-implementation-guide.md` |
| **Setting up AI tools** | `tools/`, CLAUDE.md (create in project root) |
| **Running evaluations** | `templates/evaluation-reports/`, `agent-core/evaluations/` |
| **Writing documentation** | `docs/guides/`, `templates/confluence/` |
| **Making architecture decisions** | `plan/02-architecture.md`, `docs/architecture/` |
| **Adding a new integration** | `agent-core/integrations/<name>/`, `plan/phases/` |
| **Onboarding someone** | Point them to `README.md` → `roles/README.md` → `DIRECTORY_GUIDE.md` |
| **Reviewing agent behavior** | `org/policies.md`, `roles/`, CLAUDE.md |
