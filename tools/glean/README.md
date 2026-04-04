# Glean — Enterprise Knowledge Search

## What Is Glean

Glean is an enterprise search platform that indexes and searches across all your company's tools — Jira, Confluence, Slack, Google Drive, GitHub, email, and more. It provides a unified search experience with AI-powered answers.

**Role in this project:** Glean is the knowledge retrieval layer. When the agent needs to find existing information — past decisions, relevant Jira tickets, Confluence documentation, Slack discussions — Glean finds it across all sources.

---

## Key Capabilities

### 1. Unified Cross-Platform Search

Search across all connected tools from a single query.

**Relevancy engineering use cases:**
- "What was the decision behind switching from BM25 to neural reranking?" → Finds the Confluence ADR, the Jira epic, and the Slack discussion
- "Who worked on the category boosting feature?" → Finds the PR, Jira story, and team conversations
- "What's our baseline NDCG?" → Finds the most recent evaluation report in Confluence

### 2. AI-Powered Answers

Glean doesn't just return links — it synthesizes answers from multiple sources.

**Example:**
```
Query: "How do we run relevancy evaluations?"
Answer: "Relevancy evaluations are run using the evaluation framework
  in the relevancy-engine repo. The command is:
  `python -m evaluation.run --config configs/<config>.yaml`
  Results are published to Confluence under the Evaluation Reports
  space. (Sources: Confluence: Evaluation Runbook, GitHub: README.md)"
```

### 3. People and Expertise Discovery

Glean identifies who knows what based on their activity across tools.

**Use cases:**
- "Who has expertise in query understanding?" → Shows people who've worked on related code, written docs, and discussed in Slack
- "Who should review a change to the ranking pipeline?" → Identifies contributors and reviewers

### 4. Glean API for Programmatic Access

Glean offers an API that the agent can use to search and retrieve information.

```python
import requests

response = requests.post(
    "https://your-company.glean.com/api/v1/search",
    headers={"Authorization": f"Bearer {GLEAN_API_TOKEN}"},
    json={
        "query": "relevancy evaluation baseline NDCG",
        "datasources": ["confluence", "jira", "github"],
        "pageSize": 10
    }
)
results = response.json()
```

### 5. Glean Chat

Conversational interface for multi-turn knowledge retrieval.

**Use case in agent context:**
When the agent needs to understand context that spans multiple systems, it can use Glean Chat to iteratively refine its understanding:
1. "What evaluation changes were made in Q1?"
2. "Which of those affected mobile search?"
3. "What was the outcome?"

---

## When to Use Glean vs. Other Tools

| Scenario | Use Glean | Use Instead |
|----------|----------|-------------|
| Find existing documentation | Yes | — |
| Search Jira for related tickets | Yes | Jira MCP (for structured queries) |
| Search Slack discussions | Yes | — |
| Find who knows about X | Yes | — |
| Answer "why" questions (past decisions) | Yes | — |
| Read specific Jira story details | No | Jira MCP |
| Create/update documentation | No | Confluence MCP |
| Search within current codebase | No | Claude Code (Grep/Glob) |
| Analyze data | No | Claude Code / Gemini |

**Rule of thumb:** Glean finds existing knowledge. Claude Code creates new knowledge and takes action.

---

## Setup Guide

### Step 1: Glean Workspace Setup
- Glean is configured by your IT/admin team
- Ensure these connectors are enabled: Jira, Confluence, Slack, GitHub, Google Drive
- Request API access for programmatic use

### Step 2: API Configuration
```bash
# Set environment variables
export GLEAN_API_TOKEN="your-api-token"
export GLEAN_INSTANCE="your-company.glean.com"
```

### Step 3: MCP Server for Claude Code Integration
Build a lightweight MCP server that wraps Glean's API:
```python
# mcp_servers/glean.py
# Exposes: glean_search, glean_answer, glean_people tools
# Claude Code can then call these natively
```

### Step 4: Test
```bash
claude "Search Glean for: how do we run relevancy evaluations"
# Claude Code calls Glean MCP -> returns synthesized answer with sources
```

---

## Limitations

- **Read-only**: Glean searches and retrieves but does not create or modify content
- **Index lag**: New content may take minutes to hours to appear in search results
- **Connector coverage**: Only searches tools that have been connected by admin
- **API rate limits**: Programmatic access has rate limits
- **No code execution**: Cannot run code, tests, or commands
