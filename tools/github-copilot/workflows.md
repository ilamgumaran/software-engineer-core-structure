# GitHub Copilot Workflow Recipes

## Workflow 1: Writing Evaluation Test Cases

**Scenario:** You need to add new test queries to the evaluation suite.

**Steps:**
1. Open the evaluation test file in your IDE
2. Write a comment describing the test category:
   ```python
   # Test cases for "electronics" category queries with high purchase intent
   ```
3. Start typing the first test case structure — Copilot will suggest the pattern
4. After the first case, Copilot will suggest similar cases following the same structure
5. Review and adjust relevance labels for each suggestion

**Tip:** Copilot is especially good at generating variations once you establish a pattern.

---

## Workflow 2: Implementing Metric Calculations

**Scenario:** Adding a new relevancy metric to the evaluation framework.

**Steps:**
1. Write the function signature with a clear name and type hints
2. Add a docstring describing the metric formula
3. Copilot will suggest the implementation based on the name and docstring
4. Use Copilot Chat: "Write unit tests for this function with edge cases"

---

## Workflow 3: Code Review with Copilot

**Scenario:** Reviewing a PR that changes ranking configuration logic.

**Steps:**
1. Open the changed files in your IDE
2. Use Copilot Chat: "Explain what this change does and what could go wrong"
3. Copilot analyzes the diff and explains the impact
4. Ask follow-up: "Could this change cause regressions for queries with no category?"
5. Use insights to write informed review comments

---

## Workflow 4: Writing Data Analysis Queries

**Scenario:** Building a SQL query for clickstream analysis.

**Steps:**
1. Open a `.sql` file or Python file with SQL strings
2. Write a comment describing the analysis:
   ```sql
   -- Calculate daily CTR by result position for the last 30 days,
   -- segmented by device type (mobile vs desktop)
   ```
3. Copilot suggests the full SQL query
4. Review table/column names (Copilot may not know your exact schema)
5. Adjust and run

---

## Workflow 5: Pair Programming with the Agent

**Scenario:** Claude Code made changes via a task, and you want to refine them.

**Steps:**
1. Claude Code completes a task and creates a branch
2. You check out the branch and open the changed files
3. Copilot provides context-aware completions as you refine the code
4. Use Copilot Chat to understand Claude Code's implementation choices
5. Make adjustments with Copilot's assistance
6. Commit your refinements to the same branch
