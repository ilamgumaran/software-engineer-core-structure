# Phase 6: Domain Layer + Documentation Automation (Weeks 16-18)

## Objective

Build the domain extension system so organizations can plug in their specific domain knowledge, and implement documentation automation so every agent action produces lasting documentation.

---

## Deliverables

### 6.1 Domain Extension System

- Standardized domain directory structure (`domains/<name>/`)
- Domain loading into agent context (CLAUDE.md references domain files)
- Domain-specific skill augmentation (role skills + domain skills)
- Domain-specific evaluation criteria
- Reference domain (relevancy engineering) fully documented as template

### 6.2 Documentation Automation

- Auto-generate docs from agent actions:
  - Code changes → technical documentation updates
  - Architecture decisions → ADRs
  - Data analyses → analysis reports
  - Sprint completions → progress updates
- Template system for consistent document structure
- Documentation freshness tracking
- Cross-reference maintenance

### 6.3 Knowledge Base

- Accumulate team knowledge from agent interactions
- Organize by topic (architecture, processes, decisions, analysis)
- Make searchable via Glean integration
- Support onboarding use case ("walk me through the system")

### 6.4 Domain-Specific Evaluation

- Define quality metrics per domain
- Build evaluation suites (domain-specific tests)
- Automated regression detection for domain metrics
- Report generation for domain evaluations

---

## Verification Checklist

- [ ] New domain can be added by creating `domains/<name>/` with standard files
- [ ] Agent uses domain knowledge when answering domain-specific questions
- [ ] Completing a task automatically creates/updates relevant documentation
- [ ] Documentation follows consistent templates
- [ ] Knowledge base is searchable and organized
- [ ] Domain evaluations run and produce structured reports
