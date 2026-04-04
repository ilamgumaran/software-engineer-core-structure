# Phase 1: Core Agent Foundation (Weeks 1-3)

## Objective

Build the core CLI interface, role-switching system, and AI tool configuration. This is the skeleton that every role operates through.

---

## Deliverables

### 1.1 CLI Application

**Commands:**
```bash
agent ask <question>              # Ask any question (auto-selects role)
agent task <description>          # Assign a task (multi-role execution)
agent --role <role> <command>     # Explicit role selection
agent design <description>        # Architecture/design task
agent test <description>          # Testing task
agent analyze <question>          # Data analysis task
agent review --pr <number>        # Code review (Developer + Tester + UX)
agent plan --sprint next          # Sprint planning (Project Manager)
agent scope <feature>             # Feature scoping (Product Manager)
agent ux-review <description>     # UX audit (UX Expert)
agent status                      # Current task progress
agent report                      # Generate progress report
```

### 1.2 CLAUDE.md with Role System

The CLAUDE.md file must include role definitions and selection logic:

```markdown
# Project: [Name]

## Roles
You operate as a multi-role engineering agent. When given a task:
1. Identify which role(s) are needed
2. State which role you're activating and why
3. Execute with that role's perspective and decision framework
4. Switch roles when the task requires a different perspective

Role definitions are in roles/*.md. Read them for detailed guidance.

## Domain
Domain-specific knowledge is in domains/<domain>/. Use it for
subject-matter expertise beyond general engineering skills.

[...project-specific context, conventions, commands...]
```

### 1.3 Role Selection Engine

The role selector is prompt-engineered into Claude Code's system context. It:
- Maps task keywords to primary roles
- Identifies when multiple roles are needed
- Sequences multi-role execution (PM before Architect before Developer)
- States the active role transparently

### 1.4 MCP Server Configuration

Configure MCP servers for issue tracker, documentation platform, and data access.

### 1.5 Memory Seeding

Pre-populate Claude Code's memory with team context, role usage patterns, and domain knowledge.

---

## Verification Checklist

- [ ] All CLI commands exist with `--help` documentation
- [ ] `agent ask "What roles can you play?"` lists all 9 roles
- [ ] `agent --role architect ask "..."` uses architect perspective
- [ ] `agent task "Fix a bug"` activates Developer + Tester roles
- [ ] `agent design "..."` activates Architect role
- [ ] Role switching is visible in agent output
- [ ] CLAUDE.md includes role definitions and project context
- [ ] MCP servers connect to issue tracker and documentation platform
