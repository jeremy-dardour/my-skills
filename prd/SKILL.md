---
name: prd
description: Build or refine a PRD — the WHY and WHAT of a feature. Use when the user wants to spec a feature, define capabilities, or clarify what a feature does for its users. Captures goals, user-facing behaviors, and product decisions. Excludes implementation details — those belong in the tech design.
---

Build or refine a PRD (Product Requirements Document). A PRD answers WHY and WHAT — never HOW.

## The boundary

A PRD contains:
- **Why** this feature exists (context, problem, goals)
- **What** the user can do (capabilities, behaviors, user stories)
- **Product decisions** (what's in scope, what's out, trade-offs the user experiences)
- **Open product questions** (UX choices, behavior ambiguities)

A PRD never contains:
- Library or framework choices
- Model names, class hierarchies, data structures
- API schemas, endpoints, algorithms
- Architecture patterns, wiring, config formats
- Cost estimates, token budgets, retry strategies
- Testing strategies

When you encounter implementation detail in an existing PRD, flag it for migration to the tech design doc.

## Process

### 1. Surface existing knowledge

Read the codebase and any existing docs (`docs/features/`, `docs/context.md`, ADRs) to understand what's already known. Don't ask the user for facts you can look up.

Present what you found:
- Current state of the feature (exists? partially built? greenfield?)
- Existing PRD content, if any
- Gaps: what's undefined, ambiguous, or contradictory

### 2. Draft the PRD

Write only what is known and decided. Do not fill in gaps or invent answers — leave unknowns as open questions. The grilling session will resolve them.

Write or update the PRD at `docs/features/<feature-name>/prd.md` using this structure:

```markdown
# <Feature Name> — PRD

## Context
Why this feature exists. What problem it solves. What the current state is.

## Goals
Numbered list. What success looks like from the user's perspective.

## Capability Surface
One subsection per capability. Each subsection contains:
- A short description of what the user can do and what they observe.
- **User stories** nested underneath — specific scenarios in "As a <actor>, I want <feature>, so that <benefit>" format. Cover the happy path, edge cases, and error states the user would experience.

## Decisions Made
Table: #, Decision, Context. Only product-level decisions (not implementation).

## Out of Scope
What this feature deliberately does not cover.

## Open Questions
Table: #, Question, Depends on. Only product/UX questions.
```

### 3. Start design refinement

Once the draft is written, tell the user:

> Draft PRD written. Want to grill it? I'll run `/grill-with-docs` scoped to product decisions only — no implementation detail.

If they accept, invoke `/grill-with-docs` with the argument: the PRD path and the instruction "grill the WHAT only — capabilities, behaviors, UX decisions. Redirect any HOW questions (implementation, architecture, libraries) to the tech design."
