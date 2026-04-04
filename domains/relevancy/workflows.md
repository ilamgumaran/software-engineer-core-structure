# Relevancy Engineering: Domain Workflows

## Workflow 1: Diagnose a Relevancy Problem

**Trigger:** "Users report that searching for X returns bad results"

1. **Product Manager**: Quantify the problem (how many users, what's the CTR for these queries?)
2. **Data Scientist**: Analyze clickstream data for the affected queries
3. **Developer**: Use explain API to trace ranking scores for specific queries
4. **Developer**: Check query understanding (tokenization, synonyms, spell correction)
5. **Developer**: Check recall (are relevant docs in the index?)
6. **Developer**: Check ranking (are scores correct? are business rules interfering?)
7. **Tester**: Identify affected query segments and design regression tests

## Workflow 2: Run a Relevancy Evaluation

**Trigger:** `agent eval --config v2.3 --compare baseline`

1. Load evaluation test suite (YAML with queries and relevance judgments)
2. Execute queries against both configurations
3. Calculate NDCG, MRR, P@K, R@K for each
4. Compare with statistical significance tests
5. Identify regressions (queries that got worse) and improvements
6. Generate structured report
7. Publish to Confluence and update Jira

## Workflow 3: Tune Ranking Configuration

**Trigger:** "Improve relevancy for category X"

1. **Data Scientist**: Analyze which queries underperform in category X
2. **Developer**: Identify ranking parameters that affect category queries
3. **Developer**: Create test configuration with adjusted parameters
4. **Tester**: Run evaluation comparing new config to baseline
5. **Data Scientist**: Analyze per-query results, check for regressions
6. **Product Manager**: Assess whether tradeoffs are acceptable
7. **Developer**: Create PR with the configuration change
8. **Project Manager**: Update Jira, plan A/B test rollout

## Workflow 4: Build a New Ranking Feature

**Trigger:** Jira story: "Add category-aware boosting to search ranking"

1. **Product Manager**: Define requirements and success metrics
2. **Architect**: Design how the feature integrates with the ranking pipeline
3. **Developer**: Implement the feature (new scoring component, config options)
4. **Tester**: Write unit tests, integration tests, and evaluation test cases
5. **Data Scientist**: Run offline evaluation, compare metrics
6. **Tester**: Run regression suite to ensure nothing breaks
7. **Developer**: Create PR with all changes
8. **Project Manager**: Coordinate review, plan A/B test, update Jira
