---
name: conductor-task
disable-model-invocation: true
description: Stay on the assigned task.
---

# Conductor Task

The conductor keeps the run bounded: understand the assignment, do only that work, validate the touched behavior, and stop before adjacent decisions.

## Flows

Pick exactly one flow at the start:
- **Implementation Flow** when starting an implementation task with the coding agent.
- **Review Flow** when asked to review a PR, commit, branch, or diff.
- **Review-Fix Flow** when asked to fix selected review comments or findings.

In every flow, use Break Loops when repeated validation or reasoning failures show that continuing would require a human decision.

## Implementation Flow

### 1. Pin The Assignment

Read the task source before editing: issue or ticket text, selected review comment, linked specs, repo agent instructions, current status docs, and nearby code.

Restate the assignment in 3-6 bullets:
- Requested behavior or fix
- Files or modules likely in scope
- Explicit out-of-scope work
- Validation commands expected
- Any ambiguity that would change scope

Done when the scope statement names what will change, what will not change, and the first validation target.

If the assignment is ambiguous enough that two reasonable implementations would differ in public behavior, schema, architecture, auth, migration strategy, test strategy, or CI behavior, ask before editing.

### 2. Work Inside The Scope

Make the smallest change that satisfies the pinned assignment.

Do not start adjacent issues, opportunistic refactors, or architecture cleanup. Do not change public API, database schema, migration strategy, auth behavior, test strategy, or CI behavior unless the assignment or linked spec explicitly requires it.

Done when every edit can be tied directly to the scope statement or required validation.

### 3. Validate Narrowly, Then Finally

Run the narrowest useful check first: a focused unit test, typecheck target, linter target, or reproduction command. Broaden only as needed for confidence in touched behavior.

Before declaring done, run the required final checks for the affected area. If they cannot run, report the exact command and reason.

Done when validation results are recorded, including failures and commands not run.

### 4. Close The Task

Leave a concise summary of changed files, validation results, remaining risks, and open decisions.

If committing the work, run `/log-session` before staging or committing so the session record captures the final scope, changes, and validation.

Do not mark the work complete if required checks are still failing.

## Review Flow

Use when asked to review a PR, commit, branch, or diff.

Pin the review target before inspecting: PR, commit, branch, diff, issue, spec, or merge base.

Do not edit files unless explicitly asked to fix. Report findings first, ordered by severity. For each finding, name the file and line, explain the risk, and classify the fix as small, risky, or design decision.

Done when the review report is complete, no files were changed, and any limits of the review are stated.

## Review-Fix Flow

Use when asked to fix review comments or selected review findings.

Pin the selected comment or finding before editing. Fix only that selected comment or finding. Stop before any fix that expands scope beyond it. Run the narrowest relevant checks first, then final checks for the affected area or explain why they could not run.

Done when each selected finding is either fixed, explicitly blocked by scope, or reported as already obsolete.

## Break Loops

Use in any flow when the same validation category fails twice after two different attempted fixes, or when repeated review reasoning reaches a scope or design decision the assignment did not settle.

If making progress requires a significant architecture, test strategy, migration strategy, public API, schema, auth, or CI decision that was not already specified, stop and ask.

Report:
- Failing command or unresolved reasoning question
- Current root-cause or scope hypothesis
- Two attempted fixes or two conflicting interpretations
- Two or three options for the human to choose from

Done when the report includes the command or question, hypothesis, attempted paths, and concrete next options.
