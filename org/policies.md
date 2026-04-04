# Agent Policies and Guardrails

> Replace this file with your organization's specific policies.
> These govern what the agent can and cannot do.

## Data Policies

### What the Agent CAN Access
- [ ] Source code in approved repositories
- [ ] Non-production databases (staging, dev)
- [ ] Public documentation and knowledge bases
- [ ] Anonymized/aggregated analytics data
- [ ] CI/CD logs and build artifacts

### What the Agent CANNOT Access
- [ ] Production databases (read or write)
- [ ] Customer PII (personally identifiable information)
- [ ] Authentication secrets and credentials
- [ ] Financial data or payment information
- [ ] Other teams' private repositories without permission

### What the Agent CANNOT Send to External AI APIs
- [ ] Customer data (even anonymized)
- [ ] Authentication tokens or secrets
- [ ] Internal architecture diagrams
- [ ] Unreleased product information
- [ ] HR or legal documents

## Code Policies

### What the Agent CAN Do
- [ ] Create feature branches
- [ ] Commit to feature branches
- [ ] Create pull requests
- [ ] Run tests and evaluations
- [ ] Update documentation

### What the Agent CANNOT Do
- [ ] Merge pull requests without human review
- [ ] Push directly to main/master/release branches
- [ ] Modify CI/CD pipeline configurations without review
- [ ] Delete branches, tags, or repositories
- [ ] Disable tests, linting, or security checks
- [ ] Add new external dependencies without review

## Workflow Policies

### What the Agent CAN Do
- [ ] Update issue tracker status
- [ ] Add comments to issues/stories
- [ ] Create documentation pages in designated spaces
- [ ] Post updates to designated channels

### What the Agent CANNOT Do
- [ ] Close issues (only move to "In Review")
- [ ] Modify other teams' issues
- [ ] Delete documentation pages
- [ ] Send direct messages without being asked
- [ ] Create or modify alerts/on-call schedules

## Quality Guardrails

### Before Any Code Change
- [ ] Tests must pass
- [ ] Linting must pass
- [ ] No security vulnerabilities introduced
- [ ] Code coverage does not decrease

### Before Any Domain-Specific Change
- [ ] Evaluation suite must run
- [ ] No metric regression beyond threshold
- [ ] Regressions must be documented with justification
- [ ] Change must be linked to a tracked issue

## Escalation Policies

### When the Agent Must Escalate to a Human
- [ ] Confidence below threshold on a task
- [ ] Evaluation shows regression without clear explanation
- [ ] Task requires access the agent doesn't have
- [ ] Task involves production changes
- [ ] Task affects multiple teams or services
- [ ] Task involves customer-facing changes
- [ ] Agent encounters conflicting requirements
