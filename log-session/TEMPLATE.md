# Session Log Template

Default convention to adapt when a project has no session-log convention of
its own yet.

- **Naming:** `YYYY-MM-DD-NN-slug.md`
- **Link, don't duplicate:** Anything already recorded elsewhere in the project's docs (PRDs, ADRs, a current-state doc, etc — per `CLAUDE.md`'s documentation map) belongs as a link from the session entry, not restated in it. The session log records *what happened*; other docs remain the single home for the facts themselves. to avoid duplication.

## Template

Copy this into a new file with right naming at session start and fill
it in as you go; finalize it at session end.

```markdown
# Session NN — <title> (YYYY-MM-DD)

## What was done

- <concrete actions taken this session>

## Decisions

- <decisions made → link to wherever they're formally recorded (PRD, ADR,
  etc). Write "None" if the session made none.>

## Learnings / tensions surfaced

- <non-obvious things learned, trade-offs weighed, dead-ends, user preferences discovered — skip if none>

## Status at end of session

<one short paragraph: where things stand + what's next. Mirror this into the
project's live status doc, if it has one — that doc remains the source of
truth for current status, not this entry.>
```

Keep bullets terse and factual. The session file is an immutable record of
*what happened* — don't edit past ones when things later change.
