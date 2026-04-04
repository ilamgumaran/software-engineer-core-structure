# Phase 3: Workflow Integrations (Weeks 7-9)

## Objective

Connect the agent to the team's issue tracker, documentation platform, and git hosting. Enable the agent to operate within existing workflows, not alongside them.

---

## Deliverables

### 3.1 Issue Tracker Integration (Jira / Linear / GitHub Issues)

- Read issue details, requirements, acceptance criteria
- Update issue status as the agent works
- Add structured comments with progress and results
- Create sub-tasks for complex issues
- Link issues to PRs and documentation

**MCP Server:** Exposes tools like `issue_get`, `issue_update_status`, `issue_add_comment`.

### 3.2 Documentation Platform Integration (Confluence / Notion / Markdown)

- Create pages from templates
- Update existing documentation
- Publish reports (progress, analysis, review)
- Organize pages in team hierarchy
- Cross-reference with issues and PRs

**MCP Server:** Exposes tools like `docs_create_page`, `docs_update_page`, `docs_search`.

### 3.3 Git Workflow Automation

- Branch naming conventions (from org config)
- Structured commit messages (linked to issues)
- PR creation with description templates
- Cross-referencing (issue ↔ PR ↔ docs)

**Implementation:** Claude Code native git + conventions in CLAUDE.md.

### 3.4 Cross-System Traceability

Every task produces a connected trail:
```
Issue ENG-123
  → Branch: feat/ENG-123-user-preferences
    → Commits: [ENG-123] Add preference model, [ENG-123] Add API endpoint
      → PR #204 (links to ENG-123, links to Confluence page)
        → Confluence: "User Preferences API Documentation"
          → Links back to ENG-123 and PR #204
```

---

## Verification Checklist

- [ ] `agent task --jira ENG-123` reads the issue and uses it as context
- [ ] Issue status updates automatically as the agent works
- [ ] Issue comments contain structured progress with links
- [ ] Documentation pages are created from templates
- [ ] Git operations follow configured conventions
- [ ] Cross-references are bidirectional across all systems
