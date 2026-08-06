# Ticket template

## Title

Short, names the visible result or feature area. Examples: "Layout shell +
overview + cards", "Advance + start pipeline actions".

When created as part of a batch (e.g., by `/to-tickets`), the caller may add a
`T-N:` prefix for sequencing.

## Labels

Tag by layers touched: `backend`, `frontend`, `infra`. A vertical ticket
typically carries both `backend` and `frontend`.

## Body sections

### Dependencies

First line of the body. List blocking issues by number and short title.
Omit if none.

```
Depends on #17 (entities), #18 (layout + cards).
```

### What

One paragraph: the scope of this ticket and its **visible result** — what the
user sees after it lands. This is the contract: if the visible result works,
the ticket is done.

### Backend

_Omit if the ticket has no backend work._

**Entity Changes**:
the entities that need to be created or updated for this ticket.

**Endpoints** — table with Method, Path, Body, Response, Notes. Every endpoint
this ticket introduces or modifies.

**DTOs** — code blocks showing input/output shapes relevant to this ticket.

**Business logic** — domain rules the implementation must enforce. State
machine transitions, mutability rules, validation guards, derived state
computation, error codes. Pull from the PRD's behavioral spec and the tech
design's implementation decisions. Be specific: "409 `workstream-empty` if
zero steps" not "handle edge cases."

### Frontend

_Omit if the ticket has no frontend work._

**Layout** — describe the UI this ticket builds. Reference the approved
wireframe/prototype with specific identifiers (turn, option). Include ASCII
sketches for key structures so the implementation agent doesn't need to load
the wireframe to understand the layout.

**Components** — hierarchy for this ticket. What's new, what's reused.

**Interactions** — what the user does and what happens. Button clicks, panel
transitions, mutations, refetch/invalidation behavior.

**Visual states** — card states, loading, empty, error, urgency thresholds,
selected/hover treatments. Include concrete values (colors, sizes, thresholds)
from the wireframe's design tokens.

### Testing

How to verify this ticket beyond "it works on my machine." Name:

- **What to test** — the key behaviors and edge cases worth covering.
- **How to test** — unit, integration, E2E, or manual. Match the testing
  strategy to the project's conventions.
- **Seams** — where this code integrates with the rest of the system. Test
  at these boundaries: contracts, shared types, events, interfaces.
- **Boundary conditions** — inputs at the edges: empty, max-size, malformed,
  concurrent, unauthorized.

_Omit if the ticket is trivial (e.g., config-only change)._

### Key decisions

Relevant decisions from the tech design doc, ADRs, or PRD that directly affect
this ticket's implementation. Not a full recap — only what the implementation
agent needs to know to avoid re-deriving or contradicting a settled decision.

### References

Links to the specific sections of each doc that govern this ticket:

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
- All project-specific quality checks and tests pass

## Principles

- **Self-contained.** A fresh implementation agent should be able to build this
  ticket from the ticket body plus the referenced docs. Don't assume prior context.
- **What from PRD, how from tech design.** The ticket extracts from both —
  behaviors and rules from the PRD, implementation approach from the tech
  design.
- **Concrete over abstract.** Endpoint tables, DTO shapes, ASCII layouts,
  specific error codes. "Implement the API" is not a ticket — "these 3
  endpoints with these DTOs and these error cases" is.
