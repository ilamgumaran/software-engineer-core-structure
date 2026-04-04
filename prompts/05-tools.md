# Prompt 05: Generate AI Tool Guides

## Context

You are building a multi-role software engineering agent framework. The framework uses 4 AI tools, each with distinct strengths. Now you need detailed guides and workflow recipes for each tool.

## Objective

Create a README.md and workflows.md for each of the 4 tools in `tools/`.

## Instructions

### Tool Guide Structure

Each `tools/<tool>/README.md` MUST follow this structure:

```markdown
# [Tool Name] — [One-line role description]

## What Is [Tool]
[2-3 paragraphs: what it is, how it works, what makes it distinctive]
[Role in this project: how it fits in the multi-role agent architecture]

## Key Capabilities
[3-6 numbered sections, each with description, use cases, and examples]
[Include code/config examples where applicable]

## When to Use [Tool] vs. [Other Tools]
[Comparison table: 10+ scenarios, for each: use this tool? or use which instead?]
[Rule of thumb: 1 sentence summarizing when to reach for this tool]

## Setup Guide
[3-6 numbered steps to get the tool working]
[Include actual commands and configuration snippets]

## Limitations
[5 bullet points: honest limitations that affect how you use the tool]
```

Each `tools/<tool>/workflows.md` MUST include 4-8 concrete workflow recipes:

```markdown
## Workflow N: [Name]
**Trigger:** [What initiates this workflow]
**Steps:**
1. [Numbered steps with enough detail to follow mechanically]
2. [Include which role is active if relevant]
```

### The 4 Tools

**Claude Code** (`tools/claude-code/`)

README capabilities (6 sections):
1. Persistent project context (CLAUDE.md) — with example CLAUDE.md showing role system integration
2. Memory system — with 5+ example memory commands relevant to multi-role agent
3. MCP servers — table of 4+ relevant servers (issues, docs, database, search) with config JSON example
4. Hooks — 2 hook examples relevant to agent workflow
5. Subagents — 3 use cases (research, testing, documentation)
6. Slash commands/skills — 4+ custom skills

Workflows (8 recipes):
1. Execute a Jira/issue story (10 steps, multi-role)
2. Run domain evaluation
3. Answer a codebase question
4. Analyze data
5. Document a feature
6. Onboard a new team member
7. Generate progress report
8. Code review assistance

Architecture diagram showing: Team Member → CLI → Claude Code (brain) → [CLAUDE.md, memory, MCP servers, subagents]

**GitHub Copilot** (`tools/github-copilot/`)

README capabilities (4 sections):
1. Inline code completion — with 3 relevancy-agnostic code examples
2. Copilot Chat — 4 use cases
3. Copilot for PRs — 2 use cases
4. Copilot CLI — 2 command examples

"When to use Copilot vs. Claude Code" table (10+ scenarios)

Workflows (5 recipes):
1. Writing test cases with pattern establishment
2. Implementing algorithms from specs
3. Code review with Copilot Chat
4. Writing data analysis queries
5. Pair programming with the agent

**Gemini Enterprise** (`tools/gemini-enterprise/`)

README capabilities (4 sections):
1. Large context window (1M+ tokens) — 4 use cases
2. Google Workspace integration — 4 use cases
3. LLM-as-judge at scale — with prompt template example
4. BigQuery integration — use case description

"When to use Gemini vs. Claude Code" table (10+ scenarios)

Workflows (4 recipes):
1. Bulk LLM evaluation
2. Large-scale data pattern detection
3. Document corpus review
4. Cross-reference analysis

**Glean** (`tools/glean/`)

README capabilities (5 sections):
1. Unified cross-platform search — 3 example queries
2. AI-powered answers — example query → answer with sources
3. People/expertise discovery — 2 use cases
4. Glean API — code example
5. Glean Chat — multi-turn example

"When to use Glean vs. other tools" table (10+ scenarios)

Workflows (5 recipes):
1. Context gathering before task execution
2. Finding the right reviewer
3. Answering "why" questions
4. Onboarding support
5. Incident context

## Quality Criteria

- README files should be 100-150 lines
- Workflow files should be 60-100 lines
- Comparison tables must have clear, non-overlapping recommendations
- Setup guides must include actual commands/config (not just "install the tool")
- Workflows must be step-by-step (not just descriptions)
- All examples should be role-aware and domain-agnostic (or use the reference domain)

## Verification

- 8 files exist in `tools/` (4 READMEs + 4 workflows)
- Each README has the comparison table
- Each workflows file has 4+ recipes
- Claude Code README includes the architecture diagram
- Commit with message: "Add AI tool guides with workflow recipes for Claude Code, Copilot, Gemini, Glean"
