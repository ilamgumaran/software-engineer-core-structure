# GitHub Copilot — In-IDE Pair Programming

## What Is GitHub Copilot

GitHub Copilot is an AI coding assistant integrated directly into your IDE (VS Code, JetBrains, Neovim). It provides real-time code suggestions, completions, and chat-based assistance as you type.

**Role in this project:** Copilot is the hands-on coding companion for when engineers work alongside the agent. While Claude Code handles autonomous task execution, Copilot assists engineers during manual development, code review, and exploration.

---

## Key Capabilities

### 1. Inline Code Completion

As you type, Copilot suggests completions ranging from single lines to entire functions.

**Best for:**
- Writing boilerplate code (test fixtures, config parsers, API endpoints)
- Implementing algorithms with clear patterns (metric calculations, data transformations)
- Writing repetitive code (similar handler functions, test cases)

**Relevancy engineering examples:**
```python
# Type the function signature, Copilot completes the body
def calculate_ndcg(rankings, relevance_labels, k=10):
    # Copilot suggests the full NDCG implementation

def parse_evaluation_config(config_path: str) -> EvalConfig:
    # Copilot suggests YAML parsing and validation

# Type a test function name, Copilot generates the test
def test_ndcg_perfect_ranking():
    # Copilot generates test with known-good input/output
```

### 2. Copilot Chat (IDE Sidebar)

A chat interface within the IDE for asking questions and requesting code generation.

**Best for:**
- "Explain this function" — Understanding unfamiliar code
- "Write tests for this file" — Generating test suites
- "Refactor this to use async" — Code transformation
- "What does this regex do?" — Code comprehension

**Key difference from Claude Code:** Copilot Chat operates within the IDE context (current file, open tabs). Claude Code operates across the full project and external systems.

### 3. Copilot for Pull Requests

Copilot can generate PR descriptions and suggest review comments.

**Best for:**
- Auto-generating PR descriptions from diffs
- Suggesting improvements during code review
- Summarizing changes for non-technical stakeholders

### 4. Copilot CLI (Terminal)

Copilot has a terminal component for explaining and generating shell commands.

```bash
# Explain a command
gh copilot explain "find . -name '*.yaml' -exec grep -l 'boost' {} +"

# Suggest a command
gh copilot suggest "find all evaluation configs that use boosting"
```

---

## When to Use Copilot vs. Claude Code

| Scenario | Use Copilot | Use Claude Code |
|----------|-------------|-----------------|
| Writing code in IDE | Yes | No |
| Autonomous task execution | No | Yes |
| Quick inline completions | Yes | No |
| Multi-file changes | No | Yes |
| Understanding current file | Yes | Possible |
| Understanding full codebase | Limited | Yes |
| Running evaluations | No | Yes |
| Jira/Confluence integration | No | Yes |
| PR description generation | Yes | Yes |
| Code review | Both | Both |
| Git operations | No | Yes |

**Rule of thumb:** Copilot assists *you* while you code. Claude Code acts *for you* on tasks.

---

## Setup Guide

### Step 1: Install Copilot Extension
- **VS Code:** Install "GitHub Copilot" and "GitHub Copilot Chat" extensions
- **JetBrains:** Install "GitHub Copilot" plugin from marketplace
- **Neovim:** Install `copilot.vim` or `copilot.lua`

### Step 2: Authenticate
Sign in with your GitHub account that has Copilot access (individual or enterprise).

### Step 3: Configure for Project
```json
// .vscode/settings.json
{
  "github.copilot.enable": {
    "*": true,
    "yaml": true,
    "markdown": true,
    "python": true
  }
}
```

### Step 4: Use Effectively
- Write descriptive function names and docstrings — Copilot uses them for context
- Use comments to guide suggestions: `# Calculate NDCG@10 using the standard formula`
- Accept with Tab, reject with Esc, cycle alternatives with Alt+[ / Alt+]

---

## Limitations

- **No project-wide context**: Copilot sees the current file and open tabs, not the entire codebase
- **No external integrations**: Cannot access Jira, Confluence, or databases
- **No autonomous execution**: Requires an engineer in the loop
- **Suggestion quality varies**: Works best for common patterns, less reliable for domain-specific logic
- **No persistent memory**: Each session starts fresh (no learning from past interactions)
