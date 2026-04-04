# System Architecture

## High-Level Architecture

```
+-------------------+     +-------------------+
|   CLI Interface   |     |   Web UI (Phase 7)|
+--------+----------+     +--------+----------+
         |                         |
         +------------+------------+
                      |
              +-------v--------+
              |  Task Router   |
              |  + Role Selector|
              +-------+--------+
                      |
    +--------+--------+--------+--------+-----------+
    |        |        |        |        |           |
+---v--+ +---v---+ +--v---+ +--v----+ +--v------+ +--v--------+
|Archi-| |Devel- | |Test- | |Product| |Data     | |Customer   |
|tect  | |oper   | |er    | |+UX+PM | |Scientist| |Persona    |
+---+--+ +---+---+ +--+---+ +--+----+ +--+------+ +--+--------+
    |        |        |        |          |            |
    +--------+--------+--------+----------+------------+
                      |
              +-------v--------+
              | Integration    |
              | Layer          |
              +--+---+---+---++
                 |   |   |   |
              +--v-+ v +--v-+ v
              |Git | |Issue| |Docs| |Data|
              +----+ +----+ +----+ +----+
```

## Component Details

### Task Router + Role Selector

The central orchestrator. Receives user requests, determines which role(s) to activate, and coordinates multi-role execution.

**Role selection logic:**
```
Input: "Design a new API for user preferences"
  → Parse intent: system design task
  → Primary role: Architect (system design)
  → Supporting roles: Developer (feasibility), PM (requirements check)
  → Execution order: PM first (requirements), Architect (design), Developer (prototype)

Input: "Fix the login timeout bug"
  → Parse intent: bug fix
  → Primary role: Developer (diagnose and fix)
  → Supporting roles: Tester (regression tests)
  → Execution order: Developer (fix), Tester (validate)
```

**Implementation:** Claude Code with a system prompt that includes role definitions from `roles/`, domain knowledge from `domains/`, and project context from CLAUDE.md. The role selection is part of Claude Code's reasoning, directed by well-crafted prompts.

### Role Executors

Each role executor has:
- **Perspective**: How it thinks about problems (defined in `roles/*.md`)
- **Skills**: What it can do (technical capabilities)
- **Decision framework**: How it makes choices
- **Inputs/outputs**: What it consumes and produces

The executors share the same underlying AI (Claude Code) but operate with different system prompts and decision frameworks based on the active role.

### Integration Layer

Connects to external systems. **Platform-agnostic by design** — each integration is an abstraction that maps to your specific tools.

#### Git Integration
- Branch management, structured commits, PR creation
- Convention enforcement (from CLAUDE.md and `org/` config)
- Supports: GitHub, GitLab, Bitbucket, Azure DevOps

#### Issue Tracker Integration
- Read requirements, update status, add comments, create sub-tasks
- Supports: Jira, Linear, GitHub Issues, GitLab Issues

#### Documentation Integration
- Create/update pages, publish reports, maintain knowledge base
- Supports: Confluence, Notion, GitBook, Markdown in repo

#### Data Integration
- Query data warehouses, run analysis, cache results
- Supports: BigQuery, Snowflake, Redshift, PostgreSQL

---

## Data Flow: Multi-Role Task Execution

```
1. Engineer assigns task:
   $ agent task --jira ENG-123 "Add user preference API"

2. Task Router reads Jira story → determines roles needed:
   PM (requirements) + Architect (design) + Developer (code) + Tester (tests)

3. PM Role:
   - Reads Jira story, extracts requirements and acceptance criteria
   - Validates completeness ("Missing: error handling requirements")

4. Architect Role:
   - Reads codebase to understand existing patterns
   - Designs API (endpoint, data model, storage)
   - Produces: brief design doc in PR description

5. Developer Role:
   - Creates feature branch: feat/ENG-123-user-preferences
   - Implements API following existing patterns
   - Commits with structured messages

6. Tester Role:
   - Writes unit tests for new endpoint
   - Writes integration tests for API contract
   - Runs full test suite
   - Flags: "Edge case: what if preferences exceed max size?"

7. Customer Persona Role:
   - Evaluates the new API from different user perspectives
   - "Power user would expect batch operations for preferences"
   - "New user might be confused by preference key naming conventions"

8. Integration Layer:
   - Creates PR with description (design + tests + link to Jira)
   - Updates Jira: status → In Review, adds summary comment
   - Creates/updates documentation page

9. Agent reports back:
   "PR #204 created for ENG-123. API endpoint at /api/v1/preferences
    with GET/PUT/DELETE. 12 tests passing. Jira updated.
    Flagged: max preference size not specified in requirements."
```

---

## Technology Stack

| Component | Technology | Rationale |
|-----------|-----------|-----------|
| CLI Framework | Python (Click or Typer) | Team familiarity, rich ecosystem |
| AI Orchestration | Claude Code (Anthropic) | Best code generation and multi-step reasoning |
| In-IDE Assistant | GitHub Copilot | Deep IDE integration |
| Large-Context Analysis | Gemini Enterprise (Google) | 1M+ token context, Google Workspace |
| Enterprise Search | Glean | Unified cross-tool search |
| Issue Tracker | Jira / Linear / GitHub Issues | Per-org choice (MCP server abstraction) |
| Documentation | Confluence / Notion / Markdown | Per-org choice (MCP server abstraction) |
| Git Hosting | GitHub / GitLab / Bitbucket | Per-org choice (native git + platform API) |
| Data Layer | BigQuery / Snowflake / PostgreSQL | Per-org choice (connector abstraction) |
| UI Framework (Phase 7) | React + Next.js or Streamlit | Per-org choice |
| Task Queue | Redis + Celery or SQLite (v1) | Background task management |

---

## Security Model

```
+------------------+
|    Agent         |
+------------------+
| CAN:             |
| - Read all code  |
| - Write to       |
|   feature branch |
| - Read data      |
|   (non-prod)     |
| - Create PRs     |
| - Update issues  |
| - Write docs     |
| - Run tests      |
| - Run analysis   |
+------------------+
| CANNOT:          |
| - Merge PRs      |
| - Push to main   |
| - Modify prod    |
| - Delete repos   |
| - Admin actions  |
| - Access secrets |
+------------------+
```

All production-impacting actions require human approval. The agent creates artifacts (PRs, draft docs, proposed updates) that humans review and approve.

---

## Role Routing Architecture

```
                    User Request
                         |
                         v
                  +------+------+
                  | Intent      |
                  | Classifier  |
                  +------+------+
                         |
              +----------+----------+
              |                     |
         Single Role           Multi-Role
              |                     |
              v                     v
        +-----+-----+     +--------+--------+
        | Role      |     | Role Sequencer  |
        | Executor  |     | (orchestrates   |
        +-----+-----+     |  multiple roles)|
              |            +--------+--------+
              |                     |
              v                     v
        +-----+-----+     +--------+--------+
        | Output    |     | Merged Output   |
        | Formatter |     | (combines role  |
        +-----+-----+     |  outputs)       |
              |            +--------+--------+
              |                     |
              +----------+----------+
                         |
                         v
                  +------+------+
                  | Integration |
                  | Layer       |
                  +-------------+
```

The Role Sequencer handles multi-role tasks by:
1. Determining role order (PM before Architect before Developer)
2. Passing outputs from one role as inputs to the next
3. Detecting when a role's output invalidates a prior role's assumptions
4. Merging all role outputs into a coherent response
