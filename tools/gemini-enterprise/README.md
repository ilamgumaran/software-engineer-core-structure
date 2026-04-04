# Gemini Enterprise — Large-Context Analysis

## What Is Gemini Enterprise

Gemini Enterprise is Google's AI platform available through Google Workspace. It offers a massive context window (1M+ tokens), deep integration with Google Workspace tools, and strong analytical capabilities.

**Role in this project:** Gemini handles tasks that require processing large volumes of data or documents that exceed Claude Code's context window — bulk data analysis, large document review, and LLM-as-judge evaluation at scale.

---

## Key Capabilities

### 1. Large Context Window (1M+ Tokens)

Gemini can process extremely long inputs — entire codebases, large datasets, or collections of documents in a single prompt.

**Relevancy engineering use cases:**
- Analyze a full month of evaluation reports in one pass
- Review the entire ranking pipeline codebase at once
- Process large query log exports for pattern detection
- Compare hundreds of evaluation results simultaneously

### 2. Google Workspace Integration

Gemini integrates with Google Docs, Sheets, Slides, and Drive.

**Use cases:**
- Analyze data in Google Sheets (evaluation results, metrics exports)
- Generate summary reports in Google Docs
- Search across team's Google Drive for relevant documents
- Create presentation slides from evaluation data

### 3. LLM-as-Judge at Scale

For relevancy evaluation, Gemini can assess large numbers of (query, document) pairs.

**How it works:**
```
Input: 1000 (query, document) pairs from evaluation suite
Prompt: "For each pair, rate relevance on a 0-3 scale:
         0 = not relevant, 1 = marginally relevant,
         2 = relevant, 3 = highly relevant"
Output: Relevance judgments for all 1000 pairs
```

**Advantages over Claude Code for this task:**
- Larger context window allows more pairs per batch
- Google Cloud integration for automated pipelines
- Lower per-token cost for bulk operations

### 4. Data Analysis Across Google Cloud

If your data is in BigQuery (via Google Cloud), Gemini has native integration.

**Use cases:**
- Natural language queries against BigQuery tables
- Automated data analysis with visualization
- Pattern detection across large datasets

---

## When to Use Gemini vs. Claude Code

| Scenario | Use Gemini | Use Claude Code |
|----------|-----------|-----------------|
| Bulk document analysis | Yes | Limited by context |
| LLM-as-judge (>100 pairs) | Yes | For smaller batches |
| Code generation | Limited | Yes |
| Task execution (git, CLI) | No | Yes |
| Google Sheets analysis | Yes | No |
| Jira/Confluence integration | No | Yes |
| Interactive coding | No | Yes |
| BigQuery analysis | Yes (native) | Yes (via MCP) |

**Rule of thumb:** Gemini is for analysis at scale. Claude Code is for execution and integration.

---

## Setup Guide

### Step 1: Enable Gemini Enterprise
- Requires Google Workspace Enterprise license with Gemini add-on
- Admin enables Gemini for the organization
- Users access via workspace.google.com or API

### Step 2: API Access (for Programmatic Use)
```python
# Using Google's Generative AI SDK
import google.generativeai as genai

genai.configure(api_key=os.environ["GEMINI_API_KEY"])
model = genai.GenerativeModel("gemini-1.5-pro")

# Example: Bulk relevance judgment
response = model.generate_content([
    "Rate the relevance of each query-document pair on a 0-3 scale...",
    large_evaluation_dataset
])
```

### Step 3: Integration with Agent
The agent orchestrator (Claude Code) invokes Gemini for specific tasks via API when:
- The data volume exceeds Claude Code's context window
- The task is bulk analysis (many items, same operation)
- Google Workspace data needs to be analyzed

---

## Limitations

- **No terminal/filesystem access**: Gemini cannot run commands or edit files
- **No Jira/Confluence integration**: Must go through Claude Code for these
- **Response structure**: Less reliable for generating strictly formatted outputs vs. Claude
- **Code execution**: Gemini can suggest code but cannot execute it in your environment
- **Latency**: Large-context requests take longer to process
