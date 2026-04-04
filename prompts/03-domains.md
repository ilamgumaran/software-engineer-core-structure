# Prompt 03: Generate Domain Extension System

## Context

You are building a multi-role software engineering agent framework. The roles/ directory defines HOW the agent thinks (9 perspectives, including Customer Persona). Now you need domains/ which defines WHAT the agent knows about a specific problem space.

Roles are universal. Domains are specific to the team's work. The framework ships with one reference domain (relevancy engineering) that serves as a fully worked template others can copy.

## Objective

Create `domains/README.md`, and a complete reference domain at `domains/relevancy/` with 5 files.

## Instructions

### `domains/README.md` — Domain System Overview

Write a README that explains:

1. **What a domain is**: Subject-matter expertise that supplements role skills
2. **What goes in a domain**: Table listing the 5 standard files (overview, skills, evaluation, workflows, glossary) with purpose for each
3. **Reference domain**: Point to `relevancy/` as the fully worked example
4. **Example domains**: Table listing 8+ domains (relevancy, ML platform, data engineering, backend, frontend, platform/SRE, security, mobile) with key concepts and primary roles for each
5. **Adding your domain**: Step-by-step instructions (5 steps)

### Reference Domain: `domains/relevancy/`

Create 5 files that together provide deep relevancy engineering expertise:

**`overview.md`** — Domain Overview
- What relevancy engineering is (2-3 paragraphs)
- Key concepts table (10+ terms: relevancy, ranking, NDCG, MRR, query understanding, recall, precision, evaluation, LLM-as-judge, boosting/burying)
- Why it matters (business impact)
- Primary roles in this domain (which roles activate most and for what)
- Example showing multi-role execution on a relevancy task

**`skills.md`** — Domain-Specific Skills
- Search pipeline understanding: table with 8+ components (query parser, query understanding, retrieval, scoring, semantic search, re-ranking, business rules, personalization) — each with function and common failure modes
- Ranking algorithm knowledge: BM25, TF-IDF, vector similarity, LTR, neural re-ranking, reciprocal rank fusion
- Evaluation methodology: query sets, human judgments, IR metrics, significance testing, LLM-as-judge
- Problem decomposition tree: "Bad search results" decomposed into 6+ branches
- Search engine proficiency: Elasticsearch, Solr, Vespa, vector databases

**`evaluation.md`** — Domain Evaluation
- Metrics table (6 metrics: NDCG, MRR, MAP, P@K, R@K, ERR) with what each measures and when to use
- Business metrics connection: diagram showing NDCG → CTR → conversion → revenue
- Business metrics table (6+: CTR, conversion, revenue/search, exit rate, reformulation rate, zero-result rate)
- Evaluation test suite format: YAML example showing query with expected results and relevance labels
- A/B testing methodology for the domain

**`workflows.md`** — Domain Workflows
- 4 workflows, each showing multi-role collaboration:
  1. Diagnose a relevancy problem (7 numbered steps, roles labeled)
  2. Run a relevancy evaluation (7 steps)
  3. Tune ranking configuration (8 steps with role labels)
  4. Build a new ranking feature (8 steps with role labels)

**`glossary.md`** — Domain Terminology
- Table with 25+ terms commonly used in relevancy engineering
- Each entry: term, definition (1-2 sentences)
- Include: BM25, boosting, burying, CTR, cold start, cross-encoder, bi-encoder, NDCG, MRR, MAP, P@K, R@K, query understanding, recall, re-ranking, relevance judgment, evaluation suite, ranking feature, LTR, LLM-as-judge, personalization, query reformulation, zero-result query, session, A/B test, interleaving

## Quality Criteria

- The reference domain should be detailed enough that an agent reading it can work on relevancy tasks competently
- Skills should include specific techniques, not just category names
- Workflows should explicitly label which role is active at each step
- The glossary should be comprehensive — someone new to the domain should be able to read it and understand conversations

## Verification

- 6 files exist in `domains/` (1 README + 5 domain files)
- `domains/relevancy/glossary.md` has 25+ defined terms
- `domains/relevancy/skills.md` has the search pipeline table with 8+ components
- `domains/relevancy/workflows.md` has 4 workflows with explicit role labels
- Commit with message: "Add domain extension system with relevancy engineering reference"
