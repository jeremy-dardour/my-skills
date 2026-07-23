# Ticket template

## Title

`T-N: <descriptive name>` — short, names the visible result or feature
area. Examples: "T-1: Layout shell + overview + cards", "T-3: Advance
+ start pipeline actions".

## Labels

Tag by layers touched: `backend`, `frontend`, `infra`. A vertical slice
typically carries both `backend` and `frontend`.

## Body sections

### Dependencies

First line of the body. List blocking issues by number and short title.
Omit if none.

```
Depends on #17 (entities), #18 (layout + cards).
```

### What

One paragraph: the scope of this slice and its **visible result** — what the
user sees after it lands. This is the contract: if the visible result works,
the slice is done.

### Backend

_Omit if the slice has no backend work._

**Entity Changes**:
the entities that need to be created - updated for this slice

**Endpoints** — table with Method, Path, Body, Response, Notes. Every endpoint
this slice introduces or modifies.

**DTOs** — code blocks showing input/output shapes relevant to this slice.
Only the DTOs this slice adds; don't repeat earlier slices.

**Business logic** — domain rules the implementation must enforce. State
machine transitions, mutability rules, validation guards, derived state
computation, error codes. Pull from the PRD's behavioral spec and the tech
design's implementation decisions. Be specific: "409 `workstream-empty` if
zero steps" not "handle edge cases."

### Frontend

_Omit if the slice has no frontend work._

**Layout** — describe the UI this slice builds. Reference the approved
wireframe/prototype with specific identifiers (turn, option). Include ASCII
sketches for key structures so the implementation agent doesn't need to load
the wireframe to understand the layout.

**Components** — hierarchy for this slice. What's new, what's reused from
earlier slices.

**Interactions** — what the user does and what happens. Button clicks, panel
transitions, mutations, refetch/invalidation behavior.

**Visual states** — card states, loading, empty, error, urgency thresholds,
selected/hover treatments. Include concrete values (colors, sizes, thresholds)
from the wireframe's design tokens.

### Key decisions

Relevant decisions from the tech design doc, ADRs, or PRD that directly affect
this slice's implementation. Not a full recap — only what the implementation
agent needs to know to avoid re-deriving or contradicting a settled decision.

### References

Links to the specific sections of each doc that govern this slice:

- PRD section (link + section name)
- Tech design section (link + section name)
- Wireframe (link + specific turn/option identifier)
- ADRs (link + number)

### Done when

Bulleted acceptance criteria. Each must be **verifiable** — the implementation
agent can check done vs not-done:

- Specific endpoint works with correct response shape
- UI element renders with correct data from a real API
- Edge case X returns the expected error code
- Visual treatment matches wireframe
- all project specicif quality checks & tests pass

## Principles

- **Self-contained.** A fresh implementation agent should be able to build this
  slice from the ticket plus the referenced docs. Don't assume prior context.
- **What from PRD, how from tech design.** The ticket extracts from both —
  behaviors and rules from the PRD, implementation approach from the tech
  design.
- **Concrete over abstract.** Endpoint tables, DTO shapes, ASCII layouts,
  specific error codes. "Implement the API" is not a ticket — "these 3
  endpoints with these DTOs and these error cases" is.
