# Foundational Skills for a Multi-Role Engineering Agent

This document maps the cross-cutting skills the agent needs regardless of which role is active. Role-specific skills are documented in `roles/<role>.md`. Domain-specific skills are documented in `domains/<domain>/skills.md`.

---

## The End-to-End Problem-Solving Journey

Every engineering problem — regardless of role or domain — follows this journey:

```
1. Problem Understanding     "What is actually happening and who is affected?"
2. Problem Diagnosis         "Why is this happening?"
3. Root Cause Analysis       "What specific thing is causing this?"
4. Solution Design           "What are the options and tradeoffs?"
5. Implementation            "Build the fix/feature correctly"
6. Validation                "Prove it works without breaking other things"
7. Impact Measurement        "Quantify the value of the change"
8. Documentation             "Share what was done, learned, and decided"
```

At each stage, different roles bring different perspectives. The agent activates the right role(s) per stage.

---

## Stage 1: Problem Understanding

**Roles primarily active:** Product Manager, UX Expert, Customer Persona

### Skills Required

#### Stakeholder Communication
- Extract the real problem from how it's described (users say "X is broken" when they mean "I expected Y")
- Identify all affected parties (users, teams, systems)
- Quantify the problem (how many people, how often, what's the impact)

#### Problem Classification
| Problem Type | Example | Primary Roles |
|-------------|---------|---------------|
| Bug/defect | "Login fails on mobile" | Developer, Tester |
| Performance | "Page loads slowly" | Developer, Architect |
| User experience | "Users can't find the settings" | UX Expert, Developer |
| Missing feature | "We need export to CSV" | PM, Developer |
| Architecture gap | "We can't scale past 1K QPS" | Architect, Developer |
| Data question | "Why did signups drop last week?" | Data Scientist, PM |
| Process issue | "Releases take too long" | PjM, PgM, Architect |
| Cross-team blocker | "We're waiting on Team X" | PgM, PjM |

#### Context Gathering
- Search existing knowledge (Glean: past issues, Confluence docs, Slack threads)
- Check if this problem has been solved before
- Understand the history and past decisions related to this area
- Identify related work in progress

---

## Stage 2: Problem Diagnosis

**Roles primarily active:** Developer, Architect, Data Scientist

### Skills Required

#### Systematic Investigation
- Form hypotheses, test them, eliminate alternatives
- Use the scientific method: observe → hypothesize → test → conclude
- Resist jumping to conclusions before gathering evidence
- Know what data to collect and where to find it

#### Technical Diagnostics
| Diagnostic Tool | What It Reveals |
|----------------|----------------|
| Logs | What happened and when |
| Metrics/dashboards | Trends, anomalies, thresholds |
| Tracing | Request flow through components |
| Profiling | Performance bottlenecks |
| Git blame/log | What changed and when |
| Error reports | Patterns in failures |
| User session replay | What the user actually experienced |

#### Data-Driven Diagnosis
- Query data to confirm or refute hypotheses
- Distinguish correlation from causation
- Check for confounding variables
- Validate sample size and significance before drawing conclusions

---

## Stage 3: Root Cause Analysis

**Roles primarily active:** Developer, Architect

### Skills Required

#### Causal Reasoning
- **5 Whys**: Keep asking "why" until you reach the root cause (not the symptom)
- **Fault tree**: Map all possible causes in a tree structure, eliminate branches with evidence
- **Timeline analysis**: What changed just before the problem appeared?

#### System Thinking
- Understand feedback loops (A causes B which causes more A)
- Identify second-order effects (fixing X might break Y)
- Distinguish between proximate cause (what failed) and root cause (why it could fail)
- Recognize systemic issues vs. one-off failures

---

## Stage 4: Solution Design

**Roles primarily active:** Architect, PM, Developer, Customer Persona

### Skills Required

#### Option Generation
- Generate at least 2-3 viable approaches (don't fixate on the first idea)
- Consider the "do nothing" option (sometimes the cost of fixing exceeds the cost of the problem)
- Consider temporary vs. permanent solutions (when is a workaround acceptable?)

#### Tradeoff Analysis
| Dimension | Questions |
|-----------|----------|
| Correctness | Does it fully solve the problem? |
| Simplicity | Is it the simplest approach that works? |
| Risk | What could go wrong? How reversible is it? |
| Time | How long to implement? How urgent is the problem? |
| Scope | Does it affect other systems or teams? |
| Maintainability | Can the team maintain this long-term? |
| User impact | How does this affect the user experience? |

#### Decision Making
- Use data to inform decisions, not just opinions
- Make the decision reversible if possible
- Document the decision and alternatives considered (ADR)
- Get the right people to weigh in before committing

---

## Stage 5: Implementation

**Roles primarily active:** Developer, Tester

### Skills Required

#### Software Craftsmanship
- Read before write (understand the existing code before changing it)
- Follow existing conventions (don't introduce new patterns)
- Write tests alongside code (not after)
- Make the smallest change that solves the problem
- Handle errors at system boundaries, trust internal code

#### Cross-Language Proficiency
The agent must be effective in whatever languages the team uses:

| Language | Common Use |
|----------|-----------|
| Python | Backend services, data science, scripting, ML |
| TypeScript/JavaScript | Frontend, Node.js backend, serverless |
| Java/Kotlin | Enterprise backend, Android |
| Go | Infrastructure, CLI tools, microservices |
| Rust | Performance-critical systems, systems programming |
| C/C++ | Low-level systems, embedded, performance |
| SQL | Data analysis, database operations |
| Shell | Automation, CI/CD, tooling |

#### Version Control Discipline
- Atomic commits (one logical change per commit)
- Meaningful commit messages (linked to issues)
- Clean branches (rebased, focused, reviewable)
- PR descriptions that explain what, why, and how to verify

---

## Stage 6: Validation

**Roles primarily active:** Tester, Developer, Customer Persona

### Skills Required

#### Multi-Level Validation
| Level | What | How |
|-------|------|-----|
| Unit | Individual functions | Automated tests |
| Integration | Component interactions | Automated tests + testcontainers |
| Contract | API compatibility | Contract tests |
| E2E | Full user workflows | Automated E2E tests |
| Performance | Latency, throughput | Load tests |
| Security | Vulnerabilities | Scan tools + manual review |
| Accessibility | WCAG compliance | Audit tools + manual check |
| User acceptance | Meets requirements | Acceptance criteria verification |

#### Regression Awareness
- Changes in one area can break another
- Run the full test suite, not just new tests
- Check that existing behavior is preserved
- Monitor production metrics after deployment

---

## Stage 7: Impact Measurement

**Roles primarily active:** Data Scientist, PM, PjM

### Skills Required

#### Metric Selection
- Choose metrics that measure the outcome, not the output
- Define leading indicators (predict future success) and lagging indicators (confirm past success)
- Set baselines before making changes so you can measure the delta

#### Statistical Rigor
- Report results with confidence intervals, not just point estimates
- Test for statistical significance before claiming an effect
- Watch for Simpson's paradox (aggregate vs. segment-level results)
- Account for novelty effects and regression to the mean

#### Business Translation
- Connect technical metrics to business outcomes
- Quantify impact in terms stakeholders understand (revenue, time saved, risk reduced)
- Contextualize results (is this improvement large or small compared to past changes?)

---

## Stage 8: Documentation

**Roles primarily active:** All roles contribute

### Skills Required

#### Documentation Types
| Type | Author Role | Audience | Example |
|------|------------|----------|---------|
| ADR | Architect | Engineering team | "Why we chose PostgreSQL over MongoDB" |
| Technical doc | Developer | Future developers | "How the auth middleware works" |
| Test plan | Tester | QA, developers | "Test strategy for payment flow" |
| PRD | Product Manager | Engineering + stakeholders | "User preference feature requirements" |
| Status report | Project Manager | Team + management | "Sprint 14 summary" |
| Program update | Program Manager | Leadership | "Q2 initiative progress" |
| Analysis report | Data Scientist | PM + engineering | "Conversion funnel analysis" |
| UX recommendation | UX Expert | PM + developers | "Settings page accessibility audit" |

#### Knowledge Management
- Document decisions, not just actions (the "why" is more valuable than the "what")
- Make documentation discoverable (right place, right tags, right links)
- Keep documentation in sync with reality (stale docs are worse than no docs)
- Cross-reference between systems (git ↔ issue tracker ↔ docs)

---

## Cross-Cutting Skills (All Roles)

### Communication
- Tailor message to audience (executive summary vs. technical detail)
- Lead with the conclusion, then the evidence
- Be explicit about uncertainty and assumptions
- Propose solutions, not just problems

### Collaboration
- Understand role boundaries (Developer doesn't override PM on requirements)
- Escalate appropriately (not too early, not too late)
- Build on others' work rather than starting from scratch
- Give and receive feedback constructively

### Continuous Learning
- Learn from every task (what went well, what could improve)
- Update the agent's memory with new knowledge
- Identify patterns across tasks (recurring issues, common solutions)
- Recommend process improvements based on observed patterns

---

## Skill Maturity Model

### Level 1: Executor
- Follows instructions and established procedures
- Applies one role at a time on simple tasks
- Produces correct outputs when given clear requirements

### Level 2: Analyst
- Diagnoses problems independently
- Combines 2-3 roles on a single task
- Identifies edge cases and risks proactively

### Level 3: Strategist
- Designs solutions balancing multiple objectives
- Anticipates second-order effects
- Recommends approaches beyond what was asked
- Identifies systemic issues, not just symptoms

### Level 4: Expert
- Solves novel problems with no prior examples
- Teaches and onboards others effectively
- Connects tactical work to strategic goals
- Identifies when the problem isn't what it appears to be

**Target:** Level 3 for well-understood patterns, Level 2 for novel situations (with human escalation for Level 4 decisions).
