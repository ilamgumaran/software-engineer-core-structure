# Phase 2: Developer + Tester Roles (Weeks 4-6)

## Objective

Implement the two most hands-on roles — the Developer who writes and modifies code, and the Tester who validates it. These form the inner loop of the agent's work.

---

## Deliverables

### 2.1 Developer Role: Code Generation and Modification

- Read and understand existing codebases
- Generate new code following project conventions
- Modify existing code with minimal unnecessary changes
- Create feature branches with structured naming
- Commit with meaningful messages linked to issues
- Create PRs with clear descriptions

### 2.2 Developer Role: Debugging and Bug Fixing

- Read error messages and stack traces
- Trace execution through code paths
- Reproduce and isolate issues
- Fix root causes (not just symptoms)
- Verify fix doesn't introduce regressions

### 2.3 Tester Role: Test Generation

- Write unit tests for new and existing code
- Write integration tests for component interactions
- Write E2E tests for critical user workflows
- Generate edge case tests from code analysis
- Achieve target code coverage

### 2.4 Tester Role: Quality Gates

- Run test suites and report results
- Enforce coverage thresholds
- Run linting and formatting checks
- Run security scans
- Flag quality issues before PR creation

### 2.5 Code Review (Developer + Tester Combined)

- Review PRs for correctness, conventions, and test coverage
- Identify potential bugs, security issues, and performance problems
- Suggest improvements with rationale
- Verify acceptance criteria are met

---

## Verification Checklist

- [ ] `agent task "Add a health check endpoint"` produces working code with tests
- [ ] `agent task --jira ENG-123` reads the story and implements accordingly
- [ ] `agent test "Write tests for the auth module"` produces comprehensive tests
- [ ] `agent review --pr 142` provides a multi-perspective review
- [ ] Generated code follows project conventions (verified by linter)
- [ ] Generated tests pass and cover happy + edge cases
- [ ] PRs include structured descriptions with Jira links
