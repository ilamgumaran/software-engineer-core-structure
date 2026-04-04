# Domain: Relevancy Engineering

## What Is Relevancy Engineering

Relevancy engineering is the discipline of ensuring that search and recommendation systems return the right results in the right order. It sits at the intersection of information retrieval, machine learning, data analysis, and product thinking.

## Key Concepts

| Concept | Definition |
|---------|-----------|
| **Relevancy** | How well search results match user intent |
| **Ranking** | The order in which results are presented |
| **NDCG** | Normalized Discounted Cumulative Gain — primary quality metric |
| **MRR** | Mean Reciprocal Rank — position of first relevant result |
| **Query Understanding** | Interpreting what the user meant (intent, entities, context) |
| **Recall** | Finding all relevant results (completeness) |
| **Precision** | Not returning irrelevant results (accuracy) |
| **Evaluation** | Systematic measurement of ranking quality |
| **LLM-as-Judge** | Using language models to assess relevancy at scale |
| **Boosting/Burying** | Manually promoting or demoting results |

## Why It Matters

Search is often the primary way users interact with a product. Poor relevancy directly causes:
- Lost revenue (users can't find what they want to buy)
- User frustration (repeated searches, reformulations, exits)
- Competitive disadvantage (users switch to products with better search)
- Wasted effort (merchandising can't compensate for bad ranking)

## Primary Roles in This Domain

- **Developer**: Implements ranking algorithms, pipeline components, configuration changes
- **Data Scientist**: Designs evaluation metrics, analyzes user behavior, builds ranking models
- **Tester**: Validates ranking quality through evaluation suites and regression tests
- **Architect**: Designs the search pipeline architecture (query understanding → retrieval → ranking → presentation)
- **Product Manager**: Defines relevancy goals tied to business outcomes

## How the Agent Applies This Domain

When the agent works on relevancy tasks, it combines role skills with domain knowledge:

```
Task: "Improve search results for electronics category"

As Product Manager: Define the problem (CTR is 15% below average for electronics)
As Data Scientist: Analyze click data to identify which queries underperform
As Architect: Evaluate whether the fix is config-level or architecture-level
As Developer: Implement the ranking change (e.g., category boosting)
As Tester: Run evaluation suite, compare NDCG/MRR before and after
As Project Manager: Update Jira, publish results, plan next steps
```
