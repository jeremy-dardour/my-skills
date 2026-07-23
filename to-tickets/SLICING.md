# Slicing principles

## Vertical over horizontal

Each slice cuts a narrow but complete path through every layer the feature
touches — entities, API, UI — and lands a result a user can verify in a running
app. Never split "build all endpoints" or add all entities from "build all UI" — that's horizontal,
and integration bugs pile up silently.

## Walking skeleton first

The first visual slice proves the full stack works end-to-end: data flows from
DB through API to a rendered screen. It doesn't need to be feature-complete —
it needs to be demoable for example a first diplayable element. Everything after extends a working system.

## One visible result per slice

Every slice answers: "what does the user see after this lands?" Name it
concretely: "cards appear on screen," "advancing updates the dots," "a note
appears after saving." If you can't name the visible result, the slice isn't
vertical — restructure it.

## Smallest testable increment

Each slice is the smallest unit that produces a verifiable visible result. Too
large and the implementation agent loses context. Too small and the slice
produces nothing meaningful to verify. The right size fits comfortably in a
single fresh context window.

## Dependencies flow forward

Later slices build on earlier ones, never backward. A slice should never
require changes to a previously completed slice. Each slice extends the system,
it doesn't rework it.

## UI foundation belongs in the first visual slice for a new system / Feature

Design tokens (colors, spacing, typography), shared components (buttons, badges,
avatars), and layout scaffolding belong in the first visual slice — not in a
separate "design system" issue that produces nothing visible on its own.
Reference the approved wireframe/prototype for token values.
