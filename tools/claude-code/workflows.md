# Claude Code Workflow Recipes

Concrete workflow patterns for using Claude Code in the relevancy engineering agent.

---

## Workflow 1: Execute a Jira Story

**Trigger:** `agent task --jira REL-456`

**Claude Code flow:**
1. MCP call: Read Jira story REL-456 (title, description, acceptance criteria)
2. Analyze requirements and plan implementation
3. Create feature branch: `feat/REL-456-<summary>`
4. Read relevant codebase files to understand current state
5. Make code changes
6. Run tests: `make test`
7. Commit with message: `[REL-456] <description>`
8. Create PR with evaluation results
9. MCP call: Update Jira story status to "In Review"
10. MCP call: Add Jira comment with PR link and summary

**Claude Code invocation:**
```bash
claude --task "Read Jira story REL-456 via the Jira MCP server. \
  Understand the requirements and acceptance criteria. \
  Create a feature branch, implement the changes, run tests, \
  create a PR, and update the Jira story with your progress."
```

---

## Workflow 2: Run Relevancy Evaluation

**Trigger:** `agent eval --config configs/v2.3.yaml --compare baseline`

**Claude Code flow:**
1. Read the new config file and the baseline config
2. Identify what changed between them
3. Run the evaluation suite: `python -m evaluation.run --config configs/v2.3.yaml`
4. Run baseline if cached results aren't available
5. Calculate metrics (NDCG, MRR, P@K, R@K)
6. Generate comparison table with deltas
7. Run statistical significance tests
8. Identify regressions and improvements
9. Generate structured report in markdown
10. MCP call: Create Confluence page with report (if `--publish` flag)
11. MCP call: Update Jira story with summary (if `--jira` flag)

---

## Workflow 3: Answer a Codebase Question

**Trigger:** `agent ask "How does the boosting logic work for category queries?"`

**Claude Code flow:**
1. Search codebase for boosting-related code (Grep/Glob tools)
2. Read relevant files
3. Trace the execution path from query input to boosted results
4. Formulate a clear explanation with file references
5. Include code snippets with line numbers
6. Suggest related documentation if it exists

**Key Claude Code features used:**
- File reading with `Read` tool
- Code search with `Grep` tool
- Memory system for recalling past explanations or context

---

## Workflow 4: Analyze Customer Data

**Trigger:** `agent analyze "CTR trends for electronics category last 30 days"`

**Claude Code flow:**
1. Parse the analysis request into structured parameters
2. MCP call: Query clickstream data with date and category filters
3. Calculate daily CTR with confidence intervals
4. Detect trend direction and any anomalies
5. Segment by device type, user cohort, query pattern
6. Generate insight summary with visualizations
7. Save analysis results for future reference

---

## Workflow 5: Document a Feature

**Trigger:** Automatically after a feature branch is merged, or `agent report --type feature --branch feat/REL-456`

**Claude Code flow:**
1. Read the PR description and all commits on the branch
2. Read the changed files and understand the feature
3. Read existing Confluence documentation for the affected area
4. Generate or update documentation with:
   - What was added/changed
   - How it works (with code references)
   - Configuration options
   - Testing approach
   - Related evaluation results
5. MCP call: Create/update Confluence page

---

## Workflow 6: Onboard a New Team Member

**Trigger:** `agent ask "I'm new to the team, walk me through the system"`

**Claude Code flow:**
1. Read CLAUDE.md for project overview
2. Recall relevant memories about architecture and conventions
3. Generate a structured onboarding guide:
   - Project purpose and goals
   - Architecture overview
   - Key directories and what they contain
   - How to run the system locally
   - How to run evaluations
   - Key metrics and what they mean
   - Common tasks and how to do them
   - Who to ask about what (from team memories)
4. Offer to dive deeper into any area

---

## Workflow 7: Progress Report Generation

**Trigger:** `agent report --period "last 2 weeks"` or scheduled via cron

**Claude Code flow:**
1. Read git log for the time period
2. MCP call: Read Jira stories updated in the period
3. MCP call: Read Confluence pages created/updated in the period
4. Read evaluation results from the period
5. Generate structured progress report:
   - Completed work with links
   - Key metrics changes
   - Notable findings or insights
   - Active work in progress
   - Planned next steps
6. MCP call: Publish to Confluence
7. MCP call: Post summary to Jira epic or sprint

---

## Workflow 8: Code Review Assistance

**Trigger:** `agent review --pr 142` or triggered by PR webhook

**Claude Code flow:**
1. Read PR diff and description
2. Understand the context from linked Jira story
3. Review changes for:
   - Correctness (does it do what the story asks?)
   - Conventions (matches team style?)
   - Test coverage (are changes tested?)
   - Evaluation impact (does it affect ranking?)
   - Documentation (should docs be updated?)
4. Generate review comments
5. If evaluation-impacting: suggest running an eval before merge
