---
name: to-tickets
description: Decompose a PRD + tech design document into vertical-slice GitHub issues.
disable-model-invocation: true
---

# /to-tickets

Decompose a PRD and tech design doc into **vertical slices** — end-to-end build
increments that each produce a visible, testable result — then publish them as
as the user wants (usually github issues or locally in .md files). Ask if unclear.

A vertical slice cuts through every layer the feature touches (schema, API, UI)
and lands a result a user can verify in a running app. Horizontal slices ("build
all endpoints, then all UI") are the failure mode this skill exists to prevent.

## Steps

### 1. Gather inputs

Locate and read the **PRD** (what + why) and the **tech design doc** (how).
Check args first, then conventional paths (`docs/specs/`, `docs/features/`),
then ask the user. Also read: the domain glossary (`CONTEXT.md` or equivalent),
any wireframe/prototype docs referenced by the PRD or the tech design doc, and relevant ADRs.

**Done when:** you can name every feature, behavior, endpoint, and UI element
that needs building — and the implementation decisions behind each.

### 2. Propose vertical slices

Draft an ordered list of slices following the [slicing principles](SLICING.md).
For each slice, name:

- **Title** (short, descriptive)
- **Visible result** (what the user sees after this slice lands)
- **Layers touched** (which of: entities, API, UI)
- **Blocked by** (which earlier slices, if any)

Separate **technical tracks** (pre-requisite refactoring, independent infrastructure task for example)
work into independent issues.

**Done when:** every PRD feature and every additional tech Task appears in exactly one slice, and every slice
names its visible result.

### 3. Grill the slicing

Invoke `/grilling` scoped to the slice decomposition. Seed it with these
challenges:

- **Vertical?** Does each slice touch every layer it needs? A slice that is
  "build these endpoints" with no UI, or "build these components" with no API,
  is horizontal.
- **Visible?** Can you name what the user sees after this slice?
- **Right-sized?** Could it be split without losing coherence? Is it so small it
  produces nothing meaningful? A slice should fit in a single fresh context
  window for an implementation agent.
- **Dependencies sound?** Could slices run in parallel? Are any dependencies
  artificial?
- **Walking skeleton?** Does the first visual slice prove the full stack
  end-to-end?
- **Complete?** Does every PRD behavior land in a slice? And every Technical work as well? Any gaps?

**Done when:** user has explicitly confirmed the final slice list. Do not
proceed without confirmation.

### 4. Create Tickets

For each confirmed slice, create a ticket at the location of the user's preference following the
[ticket template](../create-ticket/TICKET_TEMPLATE.md). Pull the **what** from the PRD and the
**how** from the tech design doc — each ticket is self-contained enough for a
fresh implementation agent to build from without prior context.

Create labels as needed (`backend`, `frontend`, `infra`). Label each issue by
the layers it touches. Create issues in dependency order (blockers first) so
cross-references use real issue numbers.

**Done when:** all issues are created with correct cross-references.

### 5. Link from tech design doc

Add or update a **Build sequence** section in the tech design doc with:

- Numbered issue table (link, title, scope summary)
- Dependency graph (ASCII or list)
- Independent tracks listed separately

**Done when:** the tech design doc links to every issue and documents the
dependency graph.
