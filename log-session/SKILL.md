---
name: log-session
description: Write a dated session log entry for a working session. Typically invoked from a project's own close-session skill or when the user asks to log a session.
resources:
  - TEMPLATE.md
---

# Log Session

Record what happened this session as an immutable dated entry.

## 1. Find (or create) the session log location

Check the project's `CLAUDE.md` documentation map for where session logs live.
Use whatever it points to.

If `CLAUDE.md` doesn't document a session-log location yet: ask the user where
they want session logs to live, create that folder, and add a one-line entry
to `CLAUDE.md`'s documentation map pointing to it (just the path and purpose — this skill
owns the naming convention and template, not the project docs).

## 2. Write the new session log

Create a new file — never edit past ones; these are immutable
records. Fill it in from what actually happened this session: and follow the TEMPLATE.md
