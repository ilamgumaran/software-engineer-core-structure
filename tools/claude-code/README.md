# Claude Code — Primary Execution Engine

## What Is Claude Code

Claude Code is Anthropic's CLI tool that gives Claude direct access to your terminal, filesystem, and development tools. Unlike chat-based AI assistants, Claude Code can read files, write code, run commands, manage git, and interact with external APIs — all within your project context.

**Role in this project:** Claude Code is the "brain" of the relevancy engineer agent. It orchestrates task execution, generates code, runs evaluations, and coordinates integrations with Jira, Confluence, and Git.

---

## Key Capabilities

### 1. Persistent Project Context (CLAUDE.md)

Claude Code reads a `CLAUDE.md` file from your project root on every invocation. This is the agent's long-term knowledge about your project.

**What to put in CLAUDE.md:**
```markdown
# Relevancy Engineering Project

## Project Overview
This is the relevancy engineering platform for [product].
The search ranking pipeline uses [technology] with [approach].

## Directory Structure
- src/ranking/ — Core ranking logic
- src/evaluation/ — Evaluation test suites
- configs/ — Ranking configurations
- data/ — Sample data and test fixtures

## Conventions
- Python 3.11+, black formatting, ruff linting
- Tests: pytest with --cov
- Commits: [JIRA-ID] Short description
- Branches: feat/JIRA-ID-short-description

## How to Run
- Tests: `make test`
- Evaluation: `python -m evaluation.run --config configs/v2.3.yaml`
- Lint: `make lint`

## Key Concepts
- NDCG: Our primary relevancy metric, target >0.70
- Evaluation suite: 500 queries across 12 categories
- Baseline config: configs/baseline.yaml (do not modify directly)
```

**Why it matters:** Without CLAUDE.md, every interaction starts from zero. With it, Claude Code understands your project, conventions, and constraints immediately.

### 2. Memory System

Claude Code has a persistent memory system that accumulates knowledge across sessions.

**How it works:**
- Memories are stored in `~/.claude/projects/<project>/memory/`
- Claude Code reads relevant memories at the start of each session
- You can explicitly ask Claude Code to remember things
- Memories survive across sessions and terminal restarts

**Use cases for this project:**
```
"Remember that the evaluation baseline was last updated on March 1st with config v2.1"
"Remember that the clickstream data has a 24-hour delay"
"Remember that mobile search uses a different ranking pipeline than desktop"
```

### 3. MCP Servers (Model Context Protocol)

MCP servers extend Claude Code's capabilities by connecting it to external tools and APIs.

**Relevant MCP servers for this project:**

| MCP Server | Purpose | Setup |
|-----------|---------|-------|
| Jira MCP | Read/write Jira issues | Custom server wrapping Jira REST API |
| Confluence MCP | Read/write Confluence pages | Custom server wrapping Confluence API |
| Database MCP | Query BigQuery/Snowflake | Custom server with read-only access |
| GitHub MCP | PR management beyond basic git | Official GitHub MCP server |

**Configuration in `~/.claude/settings.json`:**
```json
{
  "mcpServers": {
    "jira": {
      "command": "python",
      "args": ["-m", "mcp_servers.jira"],
      "env": {
        "JIRA_URL": "https://your-instance.atlassian.net",
        "JIRA_TOKEN": "${JIRA_API_TOKEN}"
      }
    },
    "confluence": {
      "command": "python",
      "args": ["-m", "mcp_servers.confluence"],
      "env": {
        "CONFLUENCE_URL": "https://your-instance.atlassian.net/wiki",
        "CONFLUENCE_TOKEN": "${CONFLUENCE_API_TOKEN}"
      }
    }
  }
}
```

### 4. Hooks

Hooks run shell commands in response to Claude Code events — enabling automated workflows.

**Useful hooks for this project:**

```json
{
  "hooks": {
    "postToolUse": [
      {
        "matcher": "tool == 'bash' && command.startsWith('git commit')",
        "command": "echo 'Commit created — remember to link to Jira story'"
      }
    ],
    "postResponse": [
      {
        "matcher": "true",
        "command": "echo 'Task step completed — update status if needed'"
      }
    ]
  }
}
```

### 5. Subagents

Claude Code can spawn specialized subagents for parallel or focused work.

**Use cases:**
- **Research agent**: Explore the codebase to answer questions while the main agent continues working
- **Test runner**: Run tests in the background while the main agent makes more changes
- **Documentation agent**: Generate documentation while the main agent writes code

### 6. Slash Commands and Skills

Custom skills can be defined to create reusable workflows.

**Relevant skills:**
- `/eval` — Run a relevancy evaluation
- `/analyze` — Run a data analysis
- `/report` — Generate a progress report
- `/commit` — Commit with structured message linked to Jira

---

## How Claude Code Fits in the Agent Architecture

```
Team Member
    |
    v
CLI (typer) ---> Claude Code (brain)
                      |
                      +-- Reads CLAUDE.md for project context
                      +-- Uses memory for accumulated knowledge
                      +-- Calls MCP servers for Jira/Confluence/DB
                      +-- Executes code, runs tests, manages git
                      +-- Spawns subagents for parallel work
                      +-- Responds with structured results
```

Claude Code is not just a code generator — it's a task executor that understands context, maintains state, and interacts with the team's workflow tools.

---

## Setup Guide

### Step 1: Install Claude Code
```bash
# Install via npm (recommended)
npm install -g @anthropic-ai/claude-code

# Or via brew
brew install claude-code
```

### Step 2: Authenticate
```bash
claude  # First run triggers authentication
```

### Step 3: Create CLAUDE.md
Create a `CLAUDE.md` in the project root with project context (see template above).

### Step 4: Configure MCP Servers
Add MCP server configurations to `~/.claude/settings.json` for Jira, Confluence, and database access.

### Step 5: Seed Memory
Start a Claude Code session and tell it key facts about the project that aren't captured in CLAUDE.md.

### Step 6: Test
```bash
claude "What does this project do?"
claude "Show me the ranking pipeline code"
claude "What evaluation tests do we have?"
```

---

## Limitations

- **Context window**: Claude Code has a large but finite context. For very large codebases, it needs to selectively read files rather than loading everything.
- **Cost**: Each invocation uses API tokens. Batch related work into single sessions where possible.
- **Non-determinism**: LLM outputs vary between runs. For critical evaluations, run multiple times and average.
- **No persistent processes**: Claude Code sessions are transient. Use the CLI wrapper for state management.
- **Rate limits**: API rate limits apply. Design workflows to avoid unnecessary API calls.
