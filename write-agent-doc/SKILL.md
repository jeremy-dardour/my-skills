---
name: write-agent-doc
description: Keep agent-facing docs lean by writing only preferences, behaviors, and minimal context — everything else is referenced, not copied. Use when creating or editing a CLAUDE.md, agent.md, persona file, or skill, or when onboarding an AI agent to a project.
---

# Reference, Don't Duplicate

When writing an agent-facing file (CLAUDE.md, agent.md, persona, skill), include only what is unique to *behavior*. Everything that already lives somewhere else gets a pointer, not a copy.

## What belongs in the file

- Preferences — how the agent should behave, decide, and communicate
- Behaviors — workflows, defaults, things to do/avoid that aren't documented elsewhere
- Minimal context — just enough to orient the agent, no more

## What gets referenced instead

If a fact has a natural home, link to that home and stop:

| Information | Lives in | Do |
| --- | --- | --- |
| Coding standards / style | STANDARDS.md, lint config | Reference it |
| Architecture / design decisions | ADRs | Reference the ADR |
| Project overview, setup, commands | README.md | Reference it |
| API / schema / config details | their own source/docs | Reference it |

## Rules

1. **Single source of truth** — every fact lives in exactly one place; the agent file points there.
2. **No copied content** — never paste standards, decisions, or command lists. A one-line summary plus a link is fine; a duplicated section is not.
3. **Minimal context** — include a fact inline only if it has no home and the agent needs it to behave correctly.
4. **References one level deep** — link directly to the owning file, don't chain through intermediaries.
5. **If it changes elsewhere, don't restate it here** — anything that would go stale belongs behind a link.

## Quick check before finishing

- Does any line restate something a README/STANDARDS/ADR already says? → Replace with a reference.
- Is anything here pure preference or behavior? → Keep it.
- Could a fact go stale if copied? → Link, don't copy.