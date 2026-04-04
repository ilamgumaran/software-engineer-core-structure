# Gemini Enterprise Workflow Recipes

## Workflow 1: Bulk LLM-as-Judge Evaluation

**Scenario:** You need relevance judgments for 2000 new (query, document) pairs.

**Steps:**
1. Export evaluation pairs to a structured format (CSV/JSON)
2. Batch pairs into groups of 200 (Gemini processes efficiently at this size)
3. Send each batch to Gemini with a structured judgment prompt
4. Collect and aggregate results
5. Calculate inter-annotator agreement against existing human labels
6. Feed results back into the evaluation framework

**Gemini prompt template:**
```
You are a relevance assessor for an e-commerce search engine.
For each query-document pair, rate relevance:
  3 = Highly relevant: perfect match for the query intent
  2 = Relevant: satisfies the query but not perfectly
  1 = Marginally relevant: tangentially related
  0 = Not relevant: does not satisfy the query

Respond in JSON format: [{"id": "...", "relevance": N, "reason": "..."}, ...]

Query-Document Pairs:
{pairs}
```

---

## Workflow 2: Large-Scale Data Pattern Detection

**Scenario:** Analyze 100K search queries to find patterns and segments.

**Steps:**
1. Export query logs with metadata (volume, CTR, conversion, category)
2. Upload to Google Sheets or pass via API
3. Ask Gemini to identify clusters, anomalies, and trends
4. Review Gemini's analysis and refine
5. Feed insights back into evaluation test suite design

---

## Workflow 3: Document Corpus Review

**Scenario:** Review all team's evaluation reports from the last quarter to find recurring themes.

**Steps:**
1. Gather all evaluation report pages from Confluence (exported to text)
2. Pass the full corpus to Gemini (benefits from large context window)
3. Ask for summary of trends, recurring regressions, and successful strategies
4. Use findings to prioritize next quarter's work

---

## Workflow 4: Cross-Reference Analysis

**Scenario:** Compare evaluation metrics against user behavior data to find disconnects.

**Steps:**
1. Export evaluation results (queries + NDCG scores) to Sheets
2. Export corresponding user behavior data (CTR, conversion) to same Sheet
3. Ask Gemini: "Which queries have high NDCG but low CTR? What might explain this?"
4. Gemini identifies potential issues (e.g., results are technically relevant but don't match user intent)
5. Use findings to update evaluation criteria
