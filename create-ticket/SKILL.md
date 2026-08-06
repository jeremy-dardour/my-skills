---
name: create-ticket
description: Create a single ticket in the project's issue tracker using the standard ticket template. Use when the user explicitly asks to create a ticket, file an issue, or track a piece of work.
---

# /create-ticket

Create a single ticket in the project's configured issue tracker following the
[ticket template](TICKET_TEMPLATE.md).

## Steps

### 1. Gather inputs

Extract the ticket content from the conversation context and user instructions.
The [ticket template](TICKET_TEMPLATE.md) defines the sections to populate —
omit sections that have no relevant content.

Dependencies: only from what the user explicitly states as blockers.

If the inputs are too vague to produce concrete, actionable ticket content, run
a `/grilling` session to extract the missing information before proceeding.

**Done when:** you have enough concrete detail to fill the What, at least one
layer section (Backend or Frontend), and verifiable Done-when criteria.

### 2. Determine destination

Use the project's configured issue tracker. If no tracker is configured or the
destination is ambiguous, ask the user.

**Done when:** destination is known.

### 3. Create the ticket

Format the ticket body following the [ticket template](TICKET_TEMPLATE.md) and
publish it to the issue tracker.

**Done when:** ticket exists at the destination with labels applied.

### 4. Confirm

Report the created ticket (link or path) back to the user.
