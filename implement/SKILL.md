---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets.

Use /tdd where possible, at pre-agreed seams.

Run typechecking regularly, single test files and lint and format regularly, and the full test suite once at the end.

**Commit each logical unit as you finish it — do not batch the whole change
into one commit, and never leave the work uncommitted until the end.** As soon
as a coherent slice is done and passes typecheck/lint (e.g. a hook layer, a
component, the wiring, i18n, the tests), commit it before starting the next.
Order commits so each builds on the last. Before moving to review, run
`git log --oneline <base>..HEAD` and confirm the work reads as a sequence of
small, self-contained commits — not one lump and not a pile of uncommitted
changes. This is the default, not a "when possible" nicety; it is what makes the
PR reviewable.

Once done, use /code-review to review the work.

After resolving code-review findings and final verification, use /log-session.
Commit the new session log and any required live-status update as the final
unitary commit.

Keep commits on the current branch.
