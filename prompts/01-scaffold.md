# Prompt 01: Scaffold the Framework

## Context

You are in an empty git repository. You are building a multi-role software engineering agent framework — a structural plan and prompt system that any organization can fork and customize to create an AI agent that plays 9 engineering roles (Architect, Developer, Tester, UX Expert, Product Manager, Project Manager, Program Manager, Data Scientist, Customer Persona).

## Objective

Create the complete directory structure and root files that form the skeleton of the framework.

## Instructions

### 1. Create the directory structure

Create every directory listed below. These are all empty at this stage — content files come from later prompts.

```
roles/                           # Agent role definitions (9 roles)
domains/                         # Domain-specific knowledge (extensible)
domains/relevancy/               # Reference domain: relevancy engineering
plan/                            # Planning documents
plan/phases/                     # Phase-by-phase implementation details
tools/                           # AI tool guides
tools/claude-code/               # Claude Code guide
tools/github-copilot/            # GitHub Copilot guide
tools/gemini-enterprise/         # Gemini Enterprise guide
tools/glean/                     # Glean guide
org/                             # Organization configuration templates
agent-core/                      # Future agent implementation code
agent-core/cli/                  # CLI interface
agent-core/integrations/jira/    # Jira integration
agent-core/integrations/confluence/ # Confluence integration
agent-core/integrations/git/     # Git integration
agent-core/evaluations/          # Domain evaluation framework
agent-core/data-analysis/        # Data analysis pipeline
agent-core/app-builder/          # Application scaffolding
docs/                            # Team documentation
docs/guides/                     # How-to guides
docs/architecture/               # Architecture Decision Records
templates/                       # Document generation templates
templates/confluence/            # Confluence page templates
templates/jira/                  # Jira comment templates
templates/evaluation-reports/    # Evaluation output templates
config/                          # Runtime configuration
prompts/                         # These prompts (meta — for recreating the framework)
```

### 2. Create `.gitignore`

Include patterns for: Python (`__pycache__/`, `*.egg-info/`, `.venv/`), IDE (`.idea/`, `.vscode/`), environment (`.env`, `*.credentials.json`), state (`*.db`), OS (`.DS_Store`), Node (`node_modules/`, `.next/`).

### 3. Create `LICENSE`

MIT License. Copyright line: "Multi-Role Software Engineering Agent Framework Contributors". Current year.

### 4. Initialize git

```bash
git init
git add -A
git commit -m "Initial scaffold: directory structure, .gitignore, MIT license"
```

## Verification

- All directories exist (even if empty)
- `.gitignore` covers Python, IDE, env, OS, and Node artifacts
- `LICENSE` is MIT with correct format
- Git repo is initialized with the scaffold commit
