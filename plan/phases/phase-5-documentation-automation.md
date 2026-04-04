# Phase 5: PM + UX + Customer Persona Roles (Weeks 13-15)

## Objective

Implement the product-facing roles — Product Manager (what to build and why), Project Manager (planning and tracking), Program Manager (cross-team coordination), UX Expert (design and accessibility), and Customer Persona (user perspective and reaction prediction).

---

## Deliverables

### 5.1 Product Manager Role

- Write user stories with acceptance criteria from vague requirements
- Apply prioritization frameworks (RICE, ICE, MoSCoW)
- Define success metrics and measurement plans
- Assess feature scope (MVP vs. full)
- Generate PRDs (Product Requirements Documents)

### 5.2 Project Manager Role

- Break epics into stories with effort estimates
- Plan sprints based on team capacity and priorities
- Track progress and generate status reports
- Identify and escalate risks and blockers
- Generate retrospective summaries

### 5.3 Program Manager Role

- Map cross-team dependencies
- Aggregate status across teams for leadership
- Identify resource conflicts and recommend resolution
- Generate decision memos for escalation
- Track program-level milestones

### 5.4 UX Expert Role

- Review UI code for usability issues
- Audit pages for accessibility (WCAG 2.1)
- Map user flows and identify friction points
- Recommend interaction patterns and improvements
- Review PRs that change UI from UX perspective

### 5.5 Customer Persona Role

- Manage a persona library representing key user segments
- Generate persona reaction assessments for proposed features and changes
- Create friction maps identifying pain points from each persona's perspective

---

## Verification Checklist

- [ ] `agent scope "Add social login"` produces user stories with acceptance criteria
- [ ] `agent plan --sprint next` creates a sprint plan from backlog
- [ ] `agent status` shows progress across active work
- [ ] `agent report --period "2 weeks"` generates status report
- [ ] `agent ux-review "Settings page"` identifies usability and accessibility issues
- [ ] `agent persona-review "Add social login"` generates persona reaction assessments
- [ ] Persona library contains at least 3 distinct user segment personas
- [ ] Friction maps highlight pain points per persona for a given feature
- [ ] User stories are INVEST-compliant (Independent, Negotiable, Valuable, Estimable, Small, Testable)
- [ ] Sprint plans account for capacity and dependencies
