# Glean Workflow Recipes

## Workflow 1: Context Gathering Before Task Execution

**Scenario:** Before the agent starts a task, it needs to understand the full context — past decisions, related work, existing documentation.

**Steps:**
1. Agent receives task: "Improve category boosting for electronics"
2. Search Glean: "category boosting electronics relevancy"
3. Glean returns:
   - Confluence page: "Category Boosting Strategy v2"
   - Jira epic: REL-300 "Category-specific ranking improvements"
   - Slack thread: Discussion about electronics boosting edge cases
   - PR: #98 "Previous category boosting implementation"
4. Agent reads the relevant sources to understand history
5. Agent proceeds with full context of past work and decisions

---

## Workflow 2: Finding the Right Reviewer

**Scenario:** Agent created a PR and needs to know who should review it.

**Steps:**
1. Search Glean for expertise: "ranking pipeline code review"
2. Glean identifies people who have:
   - Written code in the ranking pipeline
   - Reviewed related PRs
   - Authored relevant Confluence documentation
3. Agent suggests reviewers in the PR description

---

## Workflow 3: Answering "Why" Questions

**Scenario:** Engineer asks "Why do we use a two-stage ranking pipeline?"

**Steps:**
1. Search Glean: "two-stage ranking pipeline decision architecture"
2. Glean finds:
   - Architecture Decision Record in Confluence
   - Original Jira epic with discussion
   - Slack thread where the team debated alternatives
3. Agent synthesizes: "We moved to a two-stage pipeline in Q2 2024 (REL-200)
   because single-stage couldn't meet latency requirements at scale.
   The ADR (link) documents the alternatives considered."

---

## Workflow 4: Onboarding Support

**Scenario:** New team member asks broad questions about the team and systems.

**Steps:**
1. "What does the relevancy team work on?" → Glean searches team pages, Jira epics, recent Confluence docs
2. "Where is the evaluation data stored?" → Glean finds data architecture docs and runbooks
3. "Who should I talk to about the search pipeline?" → Glean identifies subject matter experts
4. Agent compiles a personalized onboarding guide from Glean results

---

## Workflow 5: Incident Context

**Scenario:** Relevancy metrics dropped and the team needs to investigate.

**Steps:**
1. Search Glean: "relevancy metrics drop regression"
2. Glean finds:
   - Similar past incidents and their resolutions
   - Recent deployments that might have caused the drop
   - Monitoring alerts and related Slack discussions
3. Agent provides context: "Similar drops occurred in March (REL-320) and were caused by
   a config change. The recent deploy on April 1st changed the reranker model."
