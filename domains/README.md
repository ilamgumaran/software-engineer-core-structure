# Domains

A **domain** is the specific problem space your team operates in. The framework (roles, tools, infrastructure) is domain-agnostic. The domain layer adds the subject-matter expertise that makes the agent useful for your particular work.

---

## What Goes in a Domain

Each domain directory contains:

| File | Purpose |
|------|---------|
| `overview.md` | What this domain is, key concepts, why it matters |
| `skills.md` | Domain-specific skills the agent needs (on top of role skills) |
| `evaluation.md` | How to measure quality in this domain |
| `workflows.md` | Domain-specific workflow recipes |
| `glossary.md` | Domain terminology and definitions |

---

## Reference Domain: Relevancy Engineering

The `relevancy/` directory is the reference implementation — a fully worked example showing how to define a domain. Use it as a template when adding your own.

---

## Example Domains

This framework has been designed to support any engineering domain:

| Domain | Key Concepts | Primary Roles |
|--------|-------------|---------------|
| **Relevancy Engineering** | Search ranking, NDCG, query understanding | Developer, Data Scientist, Tester |
| **ML Platform** | Model training, serving, monitoring, feature stores | Architect, Developer, Data Scientist |
| **Data Engineering** | Pipelines, data quality, warehousing, ETL | Developer, Architect, Data Scientist |
| **Backend Engineering** | APIs, microservices, databases, performance | Architect, Developer, Tester |
| **Frontend Engineering** | UI components, state management, accessibility | Developer, UX Expert, Tester |
| **Platform/SRE** | Reliability, infrastructure, incident response | Architect, Developer, Project Manager |
| **Security Engineering** | Vulnerabilities, compliance, threat modeling | Architect, Tester, Developer |
| **Mobile Engineering** | iOS/Android, cross-platform, app lifecycle | Developer, UX Expert, Tester |

---

## Adding Your Domain

1. Create `domains/<your-domain>/`
2. Copy the structure from `domains/relevancy/` as a starting point
3. Replace relevancy-specific content with your domain expertise
4. Reference your domain in the agent's CLAUDE.md configuration
5. Update `org/profile.md` with your domain context
