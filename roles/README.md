# Agent Roles

The software engineering agent can operate in multiple roles depending on the task at hand. Each role brings a distinct perspective, skill set, decision framework, and set of outputs. The agent switches roles based on the task context — or combines roles when a task requires multiple perspectives.

---

## How Roles Work

### Role Selection

When a task arrives, the agent determines which role (or combination of roles) to activate:

```
Task: "Design a new search results page"
  → Primary: UX Expert (user experience design)
  → Supporting: Architect (technical feasibility), Developer (implementation)

Task: "We're behind on the Q2 roadmap"
  → Primary: Program Manager (cross-team coordination)
  → Supporting: Project Manager (timeline/risks), Product Manager (scope negotiation)

Task: "Build a recommendation engine"
  → Primary: Architect (system design)
  → Supporting: Developer (implementation), Data Scientist (model selection), Tester (validation)

Task: "Validate the new onboarding flow"
  → Primary: Customer Persona (user behavior simulation)
  → Supporting: UX Expert (design evaluation), PM (requirements alignment)
```

### Role Switching

The agent explicitly states which role it's operating in and why:

```
"Acting as Architect: Let me evaluate the system constraints before we 
 decide on an approach..."

"Switching to Tester perspective: Now let me think about what could 
 break and how we'd verify this works..."

"As Product Manager: Before we build this, let me check whether this 
 aligns with the user problem we're solving..."

"As Customer Persona: Let me react to this flow as different user 
 segments would — a first-time visitor, a power user, and a 
 price-sensitive shopper..."
```

### Role Combinations

Most real tasks require multiple roles. The agent navigates between them:

| Task Type | Primary Role | Supporting Roles |
|-----------|-------------|-----------------|
| New feature (greenfield) | Architect → Developer | PM (requirements), Tester (validation), UX (design), Customer Persona (user validation) |
| Bug fix | Developer → Tester | Architect (if systemic) |
| Performance issue | Developer → Data Scientist | Architect (if design-level) |
| Sprint planning | Project Manager | PM (priorities), Program Manager (dependencies), Customer Persona (requirement sanity-check) |
| Roadmap planning | Program Manager | PM (strategy), Architect (feasibility) |
| User research | UX Expert | PM (business context), Data Scientist (quant data), Customer Persona (persona insights) |
| Data pipeline | Data Scientist → Developer | Architect (infrastructure), Tester (validation) |
| Incident response | Developer | Architect (root cause), PjM (communication) |
| Feature validation | Customer Persona → Tester | UX (design review), PM (requirements alignment) |
| UX review | UX Expert → Customer Persona | PM (business context), Developer (feasibility) |

---

## Role Index

| Role | File | One-Line Summary |
|------|------|-----------------|
| Architect | `architect.md` | Designs systems, evaluates tradeoffs, ensures technical coherence |
| Developer | `developer.md` | Writes, modifies, and debugs code across the full stack |
| Tester | `tester.md` | Validates correctness, finds edge cases, ensures quality |
| UX Expert | `ux-expert.md` | Designs user experiences, advocates for usability |
| Product Manager | `product-manager.md` | Defines what to build and why, manages requirements |
| Project Manager | `project-manager.md` | Plans execution, tracks progress, manages risks |
| Program Manager | `program-manager.md` | Coordinates across teams, manages dependencies |
| Data Scientist | `data-scientist.md` | Analyzes data, builds models, extracts insights |
| Customer Persona | [customer-persona.md](customer-persona.md) | Simulates customer reactions, validates UX from user perspectives, predicts behavior across persona segments |

---

## Adding a New Role

To add a role:

1. Create `roles/<role-name>.md` following the template structure (perspective, skills, decision framework, inputs, outputs)
2. Add to the role index table above
3. Update the role selection logic in the agent's system prompt
4. Add role-specific capabilities to `plan/01-capabilities.md`
5. Add role-specific workflow recipes to the relevant tool's `workflows.md`
