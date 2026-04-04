# Relevancy Engineering: Domain-Specific Skills

These skills supplement the role-level skills defined in `roles/`. They are specific to the relevancy engineering domain.

---

## Search Pipeline Understanding

The agent must understand every component in the search/ranking pipeline:

| Component | Function | Common Failure Modes |
|-----------|----------|---------------------|
| Query Parser | Tokenize, normalize, extract entities | Wrong tokenization, missed entities |
| Query Understanding | Intent classification, spell check, synonyms | Over-expansion, wrong corrections |
| Retrieval (Recall) | Find candidate documents | Missing docs, incorrect matching |
| Scoring (BM25/TF-IDF) | Text relevance scoring | Field weight misconfiguration |
| Semantic/Vector Search | Embedding-based matching | Poor embeddings, stale vectors |
| Re-ranking | Neural or learned re-ranking | Model drift, training data bias |
| Business Rules | Boosts, buries, pins, filters | Stale rules overriding relevance |
| Personalization | User-specific adjustments | Filter bubble, cold start |

## Ranking Algorithm Knowledge

- **BM25**: Term frequency, document frequency, parameters k1 and b
- **TF-IDF**: Foundation of text relevance
- **Vector similarity**: Cosine, dot product, Euclidean distance
- **Learning to Rank**: LambdaMART, XGBoost, feature-based models
- **Neural re-ranking**: Cross-encoders, bi-encoders
- **Reciprocal Rank Fusion**: Combining retrieval strategies

## Evaluation Methodology

- Design representative query sets (head, torso, tail)
- Collect and manage human relevance judgments
- Calculate IR metrics (NDCG, MRR, MAP, P@K, R@K)
- Statistical significance testing for metric comparisons
- Online-offline metric correlation
- LLM-as-judge for scalable assessment

## Problem Decomposition for Search

```
"Bad search results" could mean:
├── Query not understood (parsing/NLU failure)
├── Relevant docs not retrieved (recall failure)
├── Relevant docs ranked too low (scoring failure)
├── Business rules overriding relevance (config issue)
├── Data quality (bad product descriptions, wrong categories)
└── Presentation issue (result snippets misleading)
```

## Search Engine Proficiency

- Elasticsearch/OpenSearch: Mappings, Query DSL, analyzers, function_score
- Solr: Schema, edismax, request handlers
- Vespa: Rank profiles, YQL, ONNX integration
- Vector databases: Pinecone, Weaviate, Qdrant
