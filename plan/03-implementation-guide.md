# Step-by-Step Implementation Guide

This document explains every step in the plan: what to do, how to do it, what tools to use, and what the outcome looks like when done correctly.

---

## Phase 1: CLI Foundation

### Step 1.1: Initialize the Python Project

**What:** Set up a properly structured Python project with packaging, linting, and testing infrastructure.

**How to implement:**
```bash
# In Claude Code:
claude "Create a Python project with pyproject.toml using typer for CLI, 
  pytest for testing, black+ruff for formatting. Project name: relevancy-agent.
  Include a src/relevancy_agent/ package with __init__.py and cli.py"
```

Or manually:
```bash
mkdir -p src/relevancy_agent
touch src/relevancy_agent/__init__.py
touch src/relevancy_agent/cli.py
```

Create `pyproject.toml` with dependencies:
- `typer[all]` — CLI framework
- `rich` — Terminal output formatting
- `httpx` — HTTP client for API calls
- `pyyaml` — Configuration parsing
- `sqlalchemy` — Local state management (SQLite)
- `pytest` — Testing

**Outcome:** `pip install -e .` works. `agent --help` shows the CLI skeleton. Tests run with `pytest`.

**Verification:**
```bash
pip install -e ".[dev]"
agent --help        # Shows available commands
pytest              # Tests pass (even if just a smoke test)
```

---

### Step 1.2: Create CLAUDE.md

**What:** Write the project context file that Claude Code reads on every invocation. This is the single most impactful step for agent quality.

**How to implement:**
1. Open Claude Code in the project directory: `claude`
2. Have a conversation about the project — Claude Code will help you write CLAUDE.md
3. Or write it manually covering: project overview, directory structure, conventions, commands, key concepts

**What to include (checklist):**
- [ ] One-paragraph project description
- [ ] Directory structure with explanations
- [ ] Language and framework versions
- [ ] Code style conventions (formatter, linter, naming)
- [ ] How to run tests
- [ ] How to run evaluations (once the eval engine exists)
- [ ] Git conventions (branch naming, commit messages)
- [ ] Environment variables needed
- [ ] Common gotchas and pitfalls
- [ ] Key domain terms and their definitions

**Outcome:** When you start Claude Code and ask "What does this project do?", it gives an accurate, detailed answer without reading any files. When you ask it to write code, it follows your conventions automatically.

**Verification:**
```bash
claude "What is this project and what are its coding conventions?"
# Should answer accurately based on CLAUDE.md
claude "Create a new Python function following our conventions"
# Should use correct style, type hints, etc.
```

---

### Step 1.3: Build the CLI Commands

**What:** Implement each CLI command as a thin wrapper that routes to the appropriate agent capability.

**How to implement:**

```python
# src/relevancy_agent/cli.py
import typer
from rich.console import Console

app = typer.Typer(name="agent", help="Relevancy Engineering AI Agent")
console = Console()

@app.command()
def ask(question: str = typer.Argument(..., help="Question to ask the agent")):
    """Ask a question about the codebase, data, or systems."""
    # Route to Claude Code with the question
    # Display formatted response
    pass

@app.command()
def task(
    description: str = typer.Argument(..., help="Task description"),
    jira: str = typer.Option(None, "--jira", help="Jira story ID")
):
    """Assign a task to the agent."""
    # If --jira provided, fetch story details first
    # Create task record in local SQLite
    # Route to Claude Code with full context
    # Update task record with results
    pass

@app.command()
def eval(
    config: str = typer.Argument(..., help="Path to evaluation config"),
    compare: str = typer.Option("baseline", help="Config to compare against"),
    publish: bool = typer.Option(False, help="Publish report to Confluence")
):
    """Run a relevancy evaluation."""
    pass

@app.command()
def analyze(query: str = typer.Argument(..., help="Analysis question")):
    """Analyze customer behavior data."""
    pass

@app.command()
def status():
    """Show current task progress."""
    pass

@app.command()
def report(
    period: str = typer.Option("1w", help="Time period (e.g., 1w, 2w, 1m)"),
    publish: bool = typer.Option(False, help="Publish to Confluence")
):
    """Generate a progress report."""
    pass
```

**How Claude Code helps:** You can ask Claude Code to build this entire CLI:
```bash
claude "Build the CLI for the relevancy agent using typer. 
  Commands: ask, task, eval, analyze, status, report. 
  Each should have appropriate arguments and options. 
  Use rich for output formatting."
```

**Outcome:** All commands exist with `--help` documentation. Each command has a clear execution path even if the backend isn't fully wired yet.

**Verification:**
```bash
agent ask --help      # Shows question argument
agent task --help     # Shows description argument and --jira option
agent eval --help     # Shows config argument and --compare/--publish options
```

---

### Step 1.4: Set Up Claude Code Integration Layer

**What:** Build the Python module that invokes Claude Code programmatically from the CLI.

**How to implement:**
There are two approaches:

**Approach A: Subprocess invocation**
```python
import subprocess
import json

def invoke_claude(prompt: str, project_dir: str) -> str:
    result = subprocess.run(
        ["claude", "--output-format", "json", "-p", prompt],
        capture_output=True, text=True, cwd=project_dir
    )
    return json.loads(result.stdout)["result"]
```

**Approach B: Claude API directly (using Anthropic SDK)**
```python
from anthropic import Anthropic

client = Anthropic()

def invoke_agent(prompt: str, system_context: str) -> str:
    response = client.messages.create(
        model="claude-sonnet-4-6",
        max_tokens=4096,
        system=system_context,  # Loaded from CLAUDE.md + task-specific context
        messages=[{"role": "user", "content": prompt}]
    )
    return response.content[0].text
```

**Recommendation:** Start with Approach A (subprocess) for simplicity — it gets Claude Code's full tool access (filesystem, git, MCP servers). Move to Approach B for more control when needed.

**Outcome:** The CLI can send a request to Claude Code and receive a structured response.

**Verification:**
```bash
agent ask "What files are in the project root?"
# Returns a formatted list of files from Claude Code
```

---

### Step 1.5: Set Up Local State Management

**What:** SQLite database to track tasks, their status, and history.

**How to implement:**
```python
# src/relevancy_agent/state.py
from sqlalchemy import create_engine, Column, String, DateTime, Text
from sqlalchemy.orm import declarative_base, Session

Base = declarative_base()

class Task(Base):
    __tablename__ = "tasks"
    id = Column(String, primary_key=True)
    description = Column(Text)
    jira_id = Column(String, nullable=True)
    status = Column(String, default="pending")  # pending, in_progress, completed, failed
    created_at = Column(DateTime)
    updated_at = Column(DateTime)
    result = Column(Text, nullable=True)
    git_branch = Column(String, nullable=True)
    pr_url = Column(String, nullable=True)
    confluence_url = Column(String, nullable=True)

engine = create_engine("sqlite:///~/.relevancy-agent/state.db")
```

**Outcome:** `agent status` shows all tasks. History is preserved across sessions.

**Verification:**
```bash
agent task "Test task"
agent status
# Shows: [pending] Test task (id: abc-123)
```

---

### Step 1.6: Configure MCP Servers

**What:** Set up MCP server configuration so Claude Code can access external tools.

**How to implement:**

Add to `~/.claude/settings.json`:
```json
{
  "mcpServers": {
    "jira": {
      "command": "python",
      "args": ["-m", "relevancy_agent.mcp.jira_server"],
      "env": {
        "JIRA_URL": "https://your-instance.atlassian.net",
        "JIRA_TOKEN": "${JIRA_API_TOKEN}"
      }
    },
    "confluence": {
      "command": "python",
      "args": ["-m", "relevancy_agent.mcp.confluence_server"],
      "env": {
        "CONFLUENCE_URL": "https://your-instance.atlassian.net/wiki",
        "CONFLUENCE_TOKEN": "${CONFLUENCE_API_TOKEN}"
      }
    },
    "glean": {
      "command": "python",
      "args": ["-m", "relevancy_agent.mcp.glean_server"],
      "env": {
        "GLEAN_API_TOKEN": "${GLEAN_API_TOKEN}",
        "GLEAN_INSTANCE": "${GLEAN_INSTANCE}"
      }
    }
  }
}
```

Each MCP server is a small Python program that exposes tools to Claude Code. Claude Code discovers these tools at startup and can call them during task execution.

**Outcome:** Claude Code can natively call `jira_get_issue`, `confluence_create_page`, `glean_search` etc.

**Verification:**
```bash
claude "What MCP tools do you have available?"
# Lists jira, confluence, and glean tools
claude "Search Glean for: relevancy evaluation"
# Returns search results from Glean
```

---

### Step 1.7: Seed Claude Code Memory

**What:** Pre-populate Claude Code's memory with key project knowledge.

**How to implement:**
Start a Claude Code session and explicitly state key facts:
```
claude
> Remember that our baseline evaluation config is at configs/baseline.yaml
> Remember that evaluation metrics target: NDCG >0.70, MRR >0.60, P@5 >0.50
> Remember that the clickstream data in BigQuery has a 24-hour delay
> Remember that mobile and desktop use different ranking pipelines
> Remember that the team uses Confluence space "REL" for documentation
> Remember that Jira project "REL" is used for relevancy engineering stories
```

**Outcome:** In future sessions, Claude Code recalls these facts when relevant. If someone asks "what's our NDCG target?", Claude Code answers from memory without needing to look it up.

**Verification:**
```bash
# In a new Claude Code session (different from where memories were set):
claude "What's our target NDCG?"
# Should answer: "Your target NDCG is >0.70"
```

---

## Phase 2: Integrations

### Step 2.1: Build the Jira MCP Server

**What:** A Python MCP server that exposes Jira operations as tools Claude Code can call.

**How to implement:**
```python
# src/relevancy_agent/mcp/jira_server.py
# Using the MCP Python SDK (mcp package)

from mcp.server import Server
from mcp.types import Tool, TextContent
from jira import JIRA

server = Server("jira")
jira_client = JIRA(server=JIRA_URL, token_auth=JIRA_TOKEN)

@server.tool("jira_get_issue")
async def get_issue(issue_key: str) -> list[TextContent]:
    """Get Jira issue details including description and acceptance criteria."""
    issue = jira_client.issue(issue_key)
    return [TextContent(
        type="text",
        text=f"Title: {issue.fields.summary}\n"
             f"Status: {issue.fields.status}\n"
             f"Description: {issue.fields.description}\n"
             f"Acceptance Criteria: {issue.fields.customfield_10001}"
    )]

@server.tool("jira_update_status")
async def update_status(issue_key: str, status: str) -> list[TextContent]:
    """Update Jira issue status."""
    jira_client.transition_issue(issue_key, status)
    return [TextContent(type="text", text=f"Updated {issue_key} to {status}")]

@server.tool("jira_add_comment")
async def add_comment(issue_key: str, comment: str) -> list[TextContent]:
    """Add a comment to a Jira issue."""
    jira_client.add_comment(issue_key, comment)
    return [TextContent(type="text", text=f"Comment added to {issue_key}")]
```

**How Claude Code helps:**
```bash
claude "Build an MCP server for Jira using the mcp Python SDK. 
  Expose tools: get_issue, update_status, add_comment, create_subtask, 
  link_issue. Use the jira Python library as the backend."
```

**Outcome:** Claude Code can read Jira stories, update their status, and add comments as part of task execution.

**Verification:**
```bash
claude "Read Jira story REL-100 and summarize its requirements"
# Claude Code calls jira_get_issue("REL-100") and summarizes
```

---

### Step 2.2: Build the Confluence MCP Server

**What:** MCP server for Confluence page operations.

**How to implement:** Same pattern as Jira MCP server, exposing:
- `confluence_get_page` — Read a page by ID or title
- `confluence_create_page` — Create a new page with content
- `confluence_update_page` — Update existing page content
- `confluence_search` — Search for pages by title or content

Use `atlassian-python-api` as the backend library.

**Outcome:** Claude Code can create and update Confluence pages directly.

**Verification:**
```bash
claude "Create a Confluence page titled 'Test Page' in the REL space with some sample content"
# Creates the page and returns the URL
```

---

### Step 2.3: Implement Git Workflow Automation

**What:** Standardize git operations so every code change follows team conventions.

**How to implement:**
This doesn't need a separate MCP server — Claude Code has native git access. Instead, encode conventions in CLAUDE.md:

Add to CLAUDE.md:
```markdown
## Git Conventions
- Branch naming: feat/JIRA-ID-short-description (e.g., feat/REL-456-category-boost)
- Commit messages: [JIRA-ID] Description (e.g., [REL-456] Add category boosting parameter)
- Always create a PR, never push directly to main
- PR descriptions must include: Summary, Changes, Evaluation Results (if applicable), Jira link
- Link PRs to Jira stories in the description
```

Claude Code will follow these conventions automatically because they're in CLAUDE.md.

**Outcome:** Every branch, commit, and PR follows the team convention without explicit instructions each time.

**Verification:**
```bash
claude "Create a branch for Jira story REL-456 about adding category boosting"
# Creates: feat/REL-456-category-boost
claude "Commit the current changes for REL-456"
# Commits with: [REL-456] <appropriate description>
```

---

### Step 2.4: Wire Cross-References

**What:** When the agent completes a task, all artifacts are linked together.

**How to implement:**
Build a post-task hook that:
1. Takes the task result (branch, PR URL, Confluence URL)
2. Updates Jira story with PR link and Confluence link
3. Updates PR description with Jira and Confluence links
4. Updates Confluence page with Jira and PR links

This can be a Claude Code hook or a step in the CLI task completion flow.

**Outcome:** From any artifact (Jira story, PR, Confluence page), you can navigate to all related artifacts.

**Verification:**
- Jira story REL-456 → has link to PR #142 and Confluence report
- PR #142 → description references REL-456 and Confluence report
- Confluence report → references REL-456 and PR #142

---

## Phase 3: Evaluation Engine

### Step 3.1: Design the Evaluation Test Suite Format

**What:** Define the YAML/JSON schema for evaluation test suites.

**How to implement:**
```bash
claude "Design a YAML schema for relevancy evaluation test suites. 
  Each suite has a name, description, and list of queries. 
  Each query has an ID, query text, optional context (category, intent), 
  and expected results with relevance labels (0-3 scale).
  Create the schema file and a sample test suite."
```

**Outcome:** A documented schema and sample test suite that defines the contract for all evaluations.

**Verification:**
- Schema file validates against sample data
- Sample test suite covers multiple query types
- Schema supports extensibility for new fields

---

### Step 3.2: Build the Evaluation Runner

**What:** Python module that loads a test suite, executes queries, and collects results.

**How to implement:**
```bash
claude "Build an evaluation runner module that:
  1. Loads a YAML test suite
  2. Sends each query to a configurable search endpoint
  3. Collects ranked results
  4. Maps results to relevance judgments from the test suite
  5. Returns structured results for metric calculation
  
  Use an abstract SearchClient class so we can swap backends."
```

**Outcome:** `python -m evaluation.run --config v2.3.yaml` executes the full evaluation and outputs results.

**Verification:**
```bash
python -m evaluation.run --config configs/sample.yaml --dry-run
# Shows what would be evaluated without actually calling the search engine
python -m evaluation.run --config configs/sample.yaml
# Runs evaluation and outputs metric summary
```

---

### Step 3.3: Implement Metrics Calculator

**What:** Functions that calculate NDCG, MRR, Precision@K, Recall@K, and MAP from evaluation results.

**How to implement:**
```bash
claude "Implement relevancy metric calculations: NDCG@K, MRR, Precision@K, 
  Recall@K, and MAP. Each function takes a list of relevance scores 
  (actual ranking) and returns the metric value. Include comprehensive 
  tests with known correct values."
```

**Outcome:** Metric calculations are correct, tested, and reusable.

**Verification:**
- Unit tests pass for all metrics with known test cases
- Perfect ranking → NDCG = 1.0
- Reversed ranking → NDCG < 0.5
- Single relevant result at position 1 → MRR = 1.0

---

### Step 3.4: Build Configuration Comparator

**What:** Takes two evaluation results and produces a comparison with deltas and significance.

**How to implement:**
```bash
claude "Build a comparison module that takes two evaluation result sets 
  and produces: overall metric comparison table with deltas, per-query 
  regression list (sorted by severity), per-query improvement list, 
  and statistical significance using paired t-test or bootstrap."
```

**Outcome:** `agent eval --config v2.3 --compare baseline` produces a clear comparison report.

---

### Step 3.5: Build Report Generator

**What:** Converts evaluation results into publishable markdown reports.

**How to implement:**
Create report templates in `templates/evaluation-reports/` and a generator that fills them with evaluation data. The generator should produce markdown that renders well in both terminal and Confluence.

**Outcome:** Every evaluation automatically produces a report ready for sharing.

---

## Phase 4: Data Analysis

### Step 4.1: Build Data Connectors

**What:** Abstraction for querying BigQuery/Snowflake with parameterized templates.

**How to implement:**
```bash
claude "Build a data connector module that:
  1. Reads connection config from config/data-sources.yaml
  2. Supports BigQuery and Snowflake backends
  3. Executes parameterized SQL queries
  4. Returns results as pandas DataFrames
  5. Caches results locally with TTL to avoid repeated expensive queries"
```

**Outcome:** `data_connector.query("search_logs", "SELECT * FROM ... WHERE date > @start_date", params={"start_date": "2024-03-01"})` works.

---

### Step 4.2: Build Analysis Templates

**What:** Pre-built analysis functions for common questions.

**How to implement:**
Build a library of parameterized analyses:
```python
# src/relevancy_agent/analysis/ctr.py
def ctr_by_position(start_date, end_date, segment=None):
    """Calculate click-through rate by result position."""
    
# src/relevancy_agent/analysis/funnel.py
def search_to_purchase_funnel(start_date, end_date, category=None):
    """Calculate conversion funnel from search to purchase."""
```

Each analysis is a function that:
1. Builds and executes SQL queries
2. Processes results into a structured format
3. Generates a natural language summary

**Outcome:** `agent analyze "CTR by position for electronics this month"` runs the analysis and returns results with insights.

---

## Phase 5: Documentation Automation

### Step 5.1: Build Template Engine

**What:** System for filling Confluence page templates with dynamic data.

**How to implement:**
Use Jinja2 templates stored in `templates/confluence/`:
```python
from jinja2 import Environment, FileSystemLoader

env = Environment(loader=FileSystemLoader("templates/confluence"))
template = env.get_template("evaluation-report.md.j2")
page_content = template.render(
    config_name="v2.3",
    baseline_name="baseline",
    date="2024-03-15",
    metrics=metrics_data,
    regressions=regression_list,
    improvements=improvement_list,
    recommendations=recommendations
)
```

**Outcome:** `agent eval --config v2.3 --publish` automatically creates a well-formatted Confluence page.

---

### Step 5.2: Implement Auto-Documentation Triggers

**What:** After certain events, documentation is automatically created or updated.

**How to implement:**
Add hooks to the task completion flow:
- Post-evaluation: Generate and publish evaluation report
- Post-merge: Check if affected Confluence pages need updating
- End-of-sprint: Generate progress summary

These can be Claude Code hooks or steps in the CLI post-task flow.

**Outcome:** Documentation happens without anyone explicitly requesting it.

---

## Phase 6: UI Layer

### Step 6.1: Build REST API

**What:** HTTP API that wraps the CLI functionality.

**How to implement:**
Use FastAPI to expose the same operations as the CLI:
```python
from fastapi import FastAPI
app = FastAPI()

@app.post("/api/tasks")
async def create_task(request: TaskRequest):
    # Same logic as CLI task command
    pass

@app.get("/api/tasks/{task_id}")
async def get_task(task_id: str):
    # Read from SQLite state
    pass
```

**Outcome:** All CLI operations available via HTTP. The web UI calls these endpoints.

---

### Step 6.2: Build Web UI

**What:** Web application for visual interaction with the agent.

**How to implement:**
Start with Streamlit for rapid iteration:
```python
import streamlit as st
import requests

st.title("Relevancy Engineering Agent")

# Task creation
task_desc = st.text_input("Assign a task:")
if st.button("Submit"):
    response = requests.post(API_URL + "/api/tasks", json={"description": task_desc})
    st.success(f"Task created: {response.json()['id']}")

# Task status
tasks = requests.get(API_URL + "/api/tasks").json()
for task in tasks:
    st.write(f"[{task['status']}] {task['description']}")
```

**Outcome:** Team members can interact with the agent through a browser.

---

## Summary: Order of Implementation

| Step | What | Depends On | Primary Tool |
|------|------|-----------|-------------|
| 1.1 | Python project setup | Nothing | Claude Code |
| 1.2 | CLAUDE.md | 1.1 | Manual + Claude Code |
| 1.3 | CLI commands | 1.1 | Claude Code |
| 1.4 | Claude Code integration | 1.1, 1.2 | Claude Code |
| 1.5 | Local state (SQLite) | 1.1 | Claude Code |
| 1.6 | MCP server config | 1.1 | Manual |
| 1.7 | Seed memory | 1.2, 1.6 | Claude Code |
| 2.1 | Jira MCP server | 1.6 | Claude Code |
| 2.2 | Confluence MCP server | 1.6 | Claude Code |
| 2.3 | Git workflow automation | 1.2 | Claude Code |
| 2.4 | Cross-references | 2.1, 2.2, 2.3 | Claude Code |
| 3.1 | Eval test suite format | 1.1 | Claude Code |
| 3.2 | Eval runner | 3.1 | Claude Code |
| 3.3 | Metrics calculator | 3.1 | Claude Code |
| 3.4 | Config comparator | 3.3 | Claude Code |
| 3.5 | Report generator | 3.4 | Claude Code |
| 4.1 | Data connectors | 1.1 | Claude Code |
| 4.2 | Analysis templates | 4.1 | Claude Code |
| 5.1 | Template engine | 2.2 | Claude Code |
| 5.2 | Auto-doc triggers | 5.1 | Claude Code |
| 6.1 | REST API | 1.3, 1.5 | Claude Code |
| 6.2 | Web UI | 6.1 | Claude Code + Copilot |

Each step is designed to be independently verifiable. Complete one step, verify it works, then move to the next. Claude Code can implement most of these steps directly — just describe what you want and iterate.
