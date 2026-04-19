# Collaboration and Engagement

This file defines how humans and AI collaborators should coordinate work in this repo.

For project direction, see `02-GOAL-AND-PRINCIPLES.md`.
For project-specific system rules, see `03-DESIGN-AND-REQUIREMENT.md`.
For active work and ownership, see `04-WORKBOARD.md`.

## Core Rule

Do not begin meaningful implementation work until the lane is checked against `04-WORKBOARD.md`.

Chat is not source of truth.
Repo docs are source of truth.

## Hard Rules

1. No new meaningful work without an `IDE`, `DEC`, or `ACT` record in `04-WORKBOARD.md`.
2. No context switch without a closure or handoff note unless explicitly told to skip that step.
3. No audit without either a clear "no drift found" closeout or one or more spawned follow-up records.

## The Project Optimizes For

Every meaningful task should optimize for all of these:

1. Correct implementation
2. Source-of-truth reliability
3. Safe parallel coordination
4. Sustainable delivery with low avoidable rework

## Before Work Starts

1. Read `04-WORKBOARD.md`.
2. Confirm the item is open, shared, or assigned to you.
3. If the lane is new, add it to the workboard before implementation.
4. If the lane overlaps another owner, resolve ownership first.

## Ownership Rules

- Ownership means primary responsibility, not permanent exclusivity.
- A lane can be `Shared`, but that should be explicit.
- If you take over a lane, update the workboard first or in the same pass.
- Do not silently work inside another owner’s active lane unless it is marked shared or handed off.

## Record And Lineage Rules

The repo uses three workboard record types:

- `IDE`: idea or concept
- `DEC`: decision
- `ACT`: action

Every meaningful record should preserve lineage:

- `Origin`: the first item in the chain
- `Parent`: the immediate prior item

Use these defaults:

- new root record -> `Origin` is its own `ID`, `Parent` is `none`
- spawned record -> inherit `Origin`, set `Parent` to the immediate source

## Closure Discipline

Work must be explicitly closed, not just abandoned by context switch.

Before moving on from an item, update the workboard entry with:

- a correct status
- a short closure note
- remaining work if the item is not actually done

This also applies when a human changes direction mid-stream unless they explicitly say to skip the closeout step.

## Redirect And Interruption Rules

When work is interrupted:

- do not silently leave the old item in `In progress`
- add a `Handoff:` or `Closure:` note to the existing item
- if the new work depends on the old work, link it in `Dependencies`
- if the new work supersedes the old work, say that explicitly

## Review Expectations

Review should look for:

- bugs
- regressions
- scope drift
- missing tests
- ownership conflicts
- documentation drift

## Documentation Sync Rules

A task is not done until the relevant docs are updated in the same pass.

Use this checklist:

- if project direction changed, update `02-GOAL-AND-PRINCIPLES.md`
- if project-specific rules changed, update `03-DESIGN-AND-REQUIREMENT.md`
- if ownership, status, or backlog changed, update `04-WORKBOARD.md`
- if a meaningful historical event occurred, update `05-CHANGELOG.md`

Minimum closeout for meaningful work:

- update or close the workboard item
- capture follow-up work or residual risk
- update design/requirements docs if behavior changed
- note whether tests were run or intentionally skipped
- add a changelog entry if the work was meaningfully delivered, changed, abandoned, decided, or audited

## Audit Discipline

Repo audits are first-class work, not informal cleanup.

When auditing:

- create or use an `ACT` item in `04-WORKBOARD.md`
- define the audit scope clearly
- convert findings into explicit records when action is needed
- close the audit with a summary note even if no drift was found
