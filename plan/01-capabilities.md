# Capability Matrix: By Role

## Role: Architect

| Capability | Description | Tools Used |
|-----------|-------------|-----------|
| System design | Design components, interfaces, data flows | Claude Code |
| Technology evaluation | Assess build/buy/OSS options with tradeoffs | Claude Code + Glean |
| ADR generation | Create Architecture Decision Records | Claude Code |
| API design | Define contracts and interface specifications | Claude Code + Copilot |
| Migration planning | Plan incremental migration between systems | Claude Code |
| Performance analysis | Identify bottlenecks and optimization opportunities | Claude Code |
| Security review | Threat modeling and security architecture | Claude Code |
| Diagram generation | Architecture diagrams (component, sequence, data flow) | Claude Code |

## Role: Developer

| Capability | Description | Tools Used |
|-----------|-------------|-----------|
| Code generation | Write new features, services, components | Claude Code + Copilot |
| Code modification | Edit existing code with context awareness | Claude Code + Copilot |
| Bug fixing | Diagnose and fix defects with root cause analysis | Claude Code |
| Refactoring | Improve code structure without changing behavior | Claude Code + Copilot |
| Code review | Review PRs for correctness, style, security, tests | Claude Code |
| Dependency management | Update packages, resolve conflicts, audit security | Claude Code |
| Configuration changes | Update configs, feature flags, environment settings | Claude Code |
| Debugging | Trace issues through logs, stack traces, and code paths | Claude Code |

## Role: Tester

| Capability | Description | Tools Used |
|-----------|-------------|-----------|
| Test planning | Design test strategy with coverage goals | Claude Code |
| Unit test generation | Write unit tests for functions and classes | Claude Code + Copilot |
| Integration test generation | Write tests for component interactions | Claude Code |
| E2E test generation | Write end-to-end workflow tests | Claude Code |
| Regression testing | Run existing tests and flag failures | Claude Code |
| Performance testing | Write and run load/stress tests | Claude Code |
| Security testing | Run vulnerability scans, test for OWASP top 10 | Claude Code |
| Quality gate enforcement | Enforce coverage, lint, security gates | Claude Code |

## Role: UX Expert

| Capability | Description | Tools Used |
|-----------|-------------|-----------|
| Usability review | Evaluate UI for usability issues | Claude Code |
| Accessibility audit | Check WCAG compliance, keyboard nav, screen readers | Claude Code |
| User flow mapping | Map user journeys through the application | Claude Code |
| Interaction design | Recommend UI patterns and components | Claude Code |
| Design review | Review UI PRs for UX issues | Claude Code |
| Information architecture | Organize content and navigation | Claude Code + Glean |
| Error state design | Design helpful error messages and recovery flows | Claude Code |
| Heuristic evaluation | Evaluate against Nielsen's heuristics | Claude Code |

## Role: Product Manager

| Capability | Description | Tools Used |
|-----------|-------------|-----------|
| Requirements writing | User stories with acceptance criteria | Claude Code |
| Backlog prioritization | Apply RICE/ICE/MoSCoW to rank work | Claude Code |
| Feature scoping | Define MVP scope and future phases | Claude Code |
| Competitive analysis | Research alternatives and market position | Claude Code + Glean + Gemini |
| Success metrics | Define KPIs and measurement plans | Claude Code |
| Stakeholder communication | Status updates, decision memos | Claude Code |
| Release planning | Define release contents and communication | Claude Code |
| User research synthesis | Summarize user feedback into actionable insights | Glean + Gemini |

## Role: Project Manager

| Capability | Description | Tools Used |
|-----------|-------------|-----------|
| Sprint planning | Break work into sprints with task assignments | Claude Code |
| Task breakdown | Decompose epics into stories into tasks | Claude Code |
| Progress tracking | Monitor velocity, burn-down, completion rate | Claude Code |
| Risk management | Identify, assess, and mitigate risks | Claude Code |
| Blocker resolution | Escalate and propose solutions for blockers | Claude Code |
| Status reporting | Generate sprint/weekly/monthly status reports | Claude Code |
| Timeline forecasting | Predict completion dates from velocity | Claude Code |
| Retrospective facilitation | Summarize what worked, what didn't, action items | Claude Code |

## Role: Program Manager

| Capability | Description | Tools Used |
|-----------|-------------|-----------|
| Cross-team coordination | Track dependencies across teams | Claude Code + Glean |
| Roadmap aggregation | Unified view across team roadmaps | Claude Code |
| Dependency tracking | Map and monitor cross-team dependencies | Claude Code |
| Executive reporting | Program-level status for leadership | Claude Code |
| Resource allocation | Identify shared resource conflicts | Claude Code |
| Portfolio prioritization | Compare initiatives across teams | Claude Code |
| Decision memos | Structured escalation with options and recommendations | Claude Code |
| Change management | Plan organizational adoption of changes | Claude Code |

## Role: Data Scientist

| Capability | Description | Tools Used |
|-----------|-------------|-----------|
| Exploratory analysis | Distributions, correlations, anomalies | Claude Code + Gemini |
| SQL queries | Complex analytical queries on data warehouse | Claude Code |
| Statistical testing | Hypothesis tests, significance, confidence intervals | Claude Code |
| A/B test analysis | Experiment evaluation with proper methodology | Claude Code |
| Model building | Train, validate, and document ML models | Claude Code + Gemini |
| Feature engineering | Design and compute features for models | Claude Code |
| Visualization | Charts, dashboards, and data stories | Claude Code |
| Insight generation | Natural language summaries of data findings | Claude Code + Gemini |

## Role: Customer Persona

| Capability | Description | Tools Used |
|-----------|-------------|-----------|
| Persona construction | Build realistic multi-dimensional personas with demographics, goals, pain points, and technical literacy | Claude Code + Glean |
| Reaction prediction | Predict how specific personas react to feature changes, UI updates, or workflow modifications | Claude Code |
| Journey simulation | Walk through user journeys as specific personas, flagging friction points and delight moments | Claude Code |
| Empathy calibration | Adjust for technical literacy, emotional state, accessibility needs, and domain familiarity | Claude Code |
| Feedback translation | Convert persona reactions and simulated feedback into prioritized engineering tasks | Claude Code |
| Competitive vulnerability analysis | Identify scenarios where personas would switch to competitors based on unmet needs | Claude Code + Glean + Gemini |

---

## CLI Interface

```bash
# Role-aware commands
agent ask "How does the authentication system work?"    # Activates: Developer/Architect
agent task --jira ENG-123                               # Activates: Developer + Tester
agent design "Real-time notification system for 10K users"  # Activates: Architect
agent test "Write tests for the payment module"         # Activates: Tester
agent analyze "User conversion funnel for Q1"           # Activates: Data Scientist
agent review --pr 142                                   # Activates: Developer + Tester + UX
agent plan --sprint next                                # Activates: Project Manager
agent scope "Add social login to the platform"          # Activates: Product Manager
agent ux-review "Check the settings page for accessibility" # Activates: UX Expert
agent status                                            # Activates: Project Manager
agent report --period "last 2 weeks"                    # Activates: Project/Program Manager

# Explicit role selection
agent --role architect ask "Should we use GraphQL or REST for this API?"
agent --role data-scientist analyze "Is the recommendation model drifting?"
```

---

## Role Combination Patterns

Most tasks engage multiple roles. The agent handles this transparently:

| Task | Roles Engaged (in order) |
|------|-------------------------|
| Implement a new feature from Jira story | PM (read requirements) → Architect (assess design) → Developer (implement) → Tester (validate) → PjM (update tracking) |
| Fix a production bug | Developer (diagnose, fix) → Tester (regression test) → PjM (update status) |
| Design a new service | PM (requirements) → Architect (design) → Developer (prototype) → Tester (test plan) |
| Analyze A/B test results | Data Scientist (analyze) → PM (interpret business impact) → PjM (communicate) |
| Sprint planning | PjM (plan) → PM (prioritize) → Architect (estimate complexity) → PgM (dependencies) |
| Accessibility remediation | UX Expert (audit) → Developer (fix) → Tester (verify) |
| Cross-team initiative | PgM (coordinate) → PjM (plan per team) → PM (scope per team) |
| Onboarding new engineer | Architect (system overview) → Developer (codebase walkthrough) → PjM (team processes) |
| Validate feature with users | Customer Persona (simulate reactions) → PM (interpret feedback) → Developer (adjust implementation) |
| Pre-launch risk assessment | Customer Persona (predict behavior) → UX Expert (review) → PM (prioritize fixes) → PgM (communicate) |
