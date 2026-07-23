---
name: tech-design-doc
disable-model-invocation: true
description: Build or refine a technical design doc for a feature.
---

Build or refine a technical design document. A tech design answers HOW — never redefines the WHAT (that's the PRD's job).

## The boundary

A tech design contains:
- **Architecture** (modules, wiring, data flow)
- **Implementation decisions** (libraries, patterns, data structures, algorithms)
- **Model and schema design** (class hierarchies, API contracts, config formats)
- **Testing decisions** (what to test, at which seam)
- **Open technical questions** (implementation trade-offs, unknowns)

When you encounter product-level content (why the feature exists, what the user can do, user stories, product scope) in a tech design, flag it for migration to the PRD.

## Process

### 1. Read the PRD

The PRD is the input. Read `docs/features/<feature-name>/prd.md` to understand what needs to be built. If no PRD exists, tell the user to run `/prd` first.

### 2. Assess the codebase

Invoke `/codebase-design` to load the design vocabulary, then read the codebase — modules, interfaces, existing patterns, test structure, existing ADRs, and the tech design if one already exists.

**Challenge existing structure.** When the design touches existing modules, don't assume they should be extended as-is. Apply the deletion test: if removing a module would scatter its complexity across callers, it earns its shape; if it would simplify callers, the module is pass-through and the design should propose reshaping it. Assess whether extending a module would make it shallower — more interface for little new depth — and if so, propose deepening instead of layering on top.

Present what you found. Done when every item is addressed:
- Current implementation state (what's built, what's stubbed, what's missing)
- Existing technical decisions, if any
- Depth assessment: which existing modules the design touches are deep (keep), which are shallow or would become shallow under extension (candidates for deepening)
- Gaps: undefined interfaces, missing seams, contradictions between PRD and code
- Seams: where will you test? Prefer existing seams over new ones. Propose at the highest point possible.

### 3. Draft or update the tech design

Write only what is known and decided. Do not fill in gaps or invent answers — leave unknowns as open questions. The grilling session will resolve them.

Write or update `docs/features/<feature-name>/tech-design.md`:

```markdown
# <Feature Name> — Technical Design

## Overview
One-line: what this doc covers. Link to the PRD for WHAT and WHY.

## Architecture
How the pieces fit together. Module boundaries, data flow, wiring.

## Implementation Sections
One section per major implementation unit. Name each for what it builds.

## Testing Decisions

## Decisions Made
Table: #, Decision, Rationale.

## Open Technical Questions
Table: #, Question, Depends on.
```

### 4. Start design refinement

Once the draft is written, tell the user:

> Draft tech design written. Want to grill it? Run `/grilling` scoped to implementation decisions — architecture, testing strategy, technical trade-offs.
