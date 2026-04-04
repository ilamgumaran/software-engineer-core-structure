# Relevancy Engineering: Glossary

| Term | Definition |
|------|-----------|
| **BM25** | Best Match 25 — probabilistic text relevance scoring algorithm |
| **Boosting** | Manually increasing the ranking score of certain results |
| **Burying** | Manually decreasing the ranking score of certain results |
| **Click-Through Rate (CTR)** | Percentage of displayed results that users click on |
| **Cold Start** | When a system lacks data for new users or new items |
| **Cross-Encoder** | Neural model that scores (query, document) pairs together |
| **Bi-Encoder** | Neural model that encodes queries and documents separately for fast retrieval |
| **NDCG** | Normalized Discounted Cumulative Gain — standard graded relevance metric |
| **MRR** | Mean Reciprocal Rank — average of 1/position of first relevant result |
| **MAP** | Mean Average Precision — average precision at each relevant result |
| **P@K** | Precision at K — fraction of top-K results that are relevant |
| **R@K** | Recall at K — fraction of all relevant results found in top K |
| **Query Understanding** | NLP processing to interpret user intent from query text |
| **Recall (retrieval)** | The set of candidate documents returned before ranking |
| **Re-ranking** | A second-pass ranking stage, typically using a more expensive model |
| **Relevance Judgment** | Human (or LLM) assessment of how relevant a document is to a query |
| **Evaluation Suite** | A set of queries with relevance judgments used to measure ranking quality |
| **Feature (ranking)** | A signal used as input to a ranking model (e.g., BM25 score, click count) |
| **Learning to Rank (LTR)** | ML approach to ranking using labeled data and ranking loss functions |
| **LLM-as-Judge** | Using a language model to generate relevance judgments at scale |
| **Personalization** | Adjusting search results based on individual user signals |
| **Query Reformulation** | When a user changes their query after unsatisfactory results |
| **Zero-Result Query** | A query that returns no results — an absolute failure |
| **Session** | A sequence of user actions (searches, clicks, purchases) in one visit |
| **A/B Test** | Randomized experiment comparing two ranking configurations with live traffic |
| **Interleaving** | Experiment method that mixes results from two rankers in one result list |
