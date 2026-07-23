---
name: tech-design-doc
description: Build or refine a technical design doc — the HOW of a feature. Use when the user wants to plan implementation, make architecture decisions, or define how a feature works internally. Reads from an existing PRD for the WHAT; focuses on implementation, testing, and technical trade-offs.
---

Build or refine a technical design document. A tech design answers HOW — never redefines the WHAT (that's the PRD's job).

## The boundary

A tech design contains:
- **Architecture** (modules, wiring, data flow)
- **Implementation decisions** (libraries, patterns, data structures, algorithms)
- **Model and schema design** (class hierarchies, API contracts, config formats)
- **Testing decisions** (what to test, at which seam)
- **Open technical questions** (implementation trade-offs, unknowns)

A tech design never contains:
- Why the feature exists (that's the PRD's Context/Goals)
- What the user can do (that's the PRD's Capability Surface)
- User stories (those belong in the PRD)
- Product-level scope decisions (those belong in the PRD's Out of Scope)

When you encounter product-level content in a tech design, flag it for migration to the PRD.

## Process

### 1. Read the PRD

The PRD is the input. Read `docs/features/<feature-name>/prd.md` to understand what needs to be built. If no PRD exists, tell the user to run `/prd` first.

### 2. Surface existing knowledge

Read the codebase — modules, interfaces, existing patterns, test structure — to understand the current implementation landscape. Check existing ADRs and the tech design if one already exists.

Present what you found:
- Current implementation state (what's built, what's stubbed, what's missing)
- Existing technical decisions, if any
- Gaps: undefined interfaces, missing seams, contradictions between PRD and code
- Seams: where will you test? Prefer existing seams over new ones. Propose at the highest point possible.

### 3. Load design vocabulary

Invoke `/codebase-design` to load the shared vocabulary before writing.

### 4. Draft or update the tech design

Write only what is known and decided. Do not fill in gaps or invent answers — leave unknowns as open questions. The grilling session will resolve them.

Write or update the tech design at `docs/features/<feature-name>/tech-design.md` using this structure:

```markdown
# <Feature Name> — Technical Design

## Overview
One-line: what this doc covers. Link to the PRD for WHAT and WHY.

## Architecture
How the pieces fit together. Module boundaries, data flow, wiring.

## Implementation Sections
One section per major implementation unit. Name each for what it builds, not for a PRD capability. Include model/schema design where relevant.

## Testing Decisions
- What makes a good test for this feature (seams, boundaries)
- Which modules get tested and at which level
- Prior art: similar test patterns already in the codebase

## Decisions Made
Table: #, Decision, Rationale. Implementation-level decisions only.

## Open Technical Questions
Table: #, Question, Depends on. Implementation unknowns only.
```

### 5. Start design refinement

Once the draft is written, tell the user:

> Draft tech design written. Want to grill it? I'll run `/grill-with-docs` scoped to implementation decisions only — no product questions.

If they accept, invoke `/grill-with-docs` with the argument: the tech design path and the instruction "grill the HOW only — architecture, implementation decisions, testing strategy, technical trade-offs. Redirect any WHAT questions (capabilities, user stories, UX) to the PRD."
