# Relevancy Engineering: Evaluation

## Metrics

| Metric | Measures | Best For |
|--------|----------|----------|
| NDCG@K | Graded relevance with position discount | Overall ranking quality |
| MRR | Position of first relevant result | Navigational queries |
| MAP | Average precision across recall levels | Balanced precision/recall |
| Precision@K | Relevant results in top K | Top-of-funnel quality |
| Recall@K | Coverage of relevant results | Completeness |
| ERR | Expected reciprocal rank | User satisfaction model |

## Business Metrics Connection

```
NDCG improvement → CTR improvement → Conversion improvement → Revenue impact
```

| Business Metric | Connection to Relevancy |
|----------------|------------------------|
| CTR | Direct measure of result attractiveness |
| Conversion Rate | End-to-end search effectiveness |
| Revenue per Search | Business value of search |
| Search Exit Rate | Indicates search failure |
| Reformulation Rate | Initial search didn't work |
| Zero-Result Rate | Absolute recall failure |

## Evaluation Test Suite Format

```yaml
name: "Category Query Evaluation"
queries:
  - id: "cat-001"
    query: "wireless headphones"
    context:
      category: "electronics"
    expected:
      - doc_id: "prod-123"
        relevance: 3  # highly relevant
      - doc_id: "prod-456"
        relevance: 2  # relevant
```

## A/B Testing for Relevancy

- Sample size calculation based on expected effect size
- Guardrail metrics: latency, error rate, revenue (must not degrade)
- Segment analysis: mobile vs. desktop, head vs. tail queries
- Duration: minimum 1-2 weeks to capture weekly patterns
