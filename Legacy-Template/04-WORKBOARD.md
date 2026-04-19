# Project Name - Workboard

This is the operational source of truth for active work, ownership, priorities, open decisions, and audit activity.

Use this file for:

- live ideas and concepts
- decisions that need resolution or have resolved direction
- actions such as implementation, audit, review, cleanup, or migration work
- ownership and reviewer assignment
- dependencies and sequencing
- closure notes and handoff notes

## Record Types

- `IDE`: idea or concept
- `DEC`: decision
- `ACT`: action

## Lineage Rules

Every meaningful record must preserve:

1. the first source in the chain
2. the immediate previous source

Required fields:

- `ID`
- `Origin`
- `Parent`

Rules:

- Root item: `Origin` is the same as `ID`, and `Parent` is `none`
- Spawned item: inherit `Origin` from the parent item
- Spawned item: set `Parent` to the immediate item that spawned it

## Shared Labels

Priority labels:

- `Must`
- `Should`
- `Nice`

Recommended tags:

- `Area`: [define your project’s short list]
- `Audit scope`: `Runtime`, `Docs`, `UX`, `Tests`, `Persistence` or project equivalents

## Closure Rules

An action is not safely closed unless it has both:

1. a correct status
2. a closure note

Suggested closeout labels:

- `Closure:`
- `Remaining:`
- `Follow-up:`
- `Handoff:`

## Templates

```md
### IDE-XXX - Title

- ID: IDE-XXX
- Type: Idea
- Origin: IDE-XXX
- Parent: none
- Area:
- Priority:
- Status: Proposed
- Owner:
- Reviewer:
- Dependencies:
- Summary:
- Why it matters:
- Follow-up:
```

```md
### DEC-XXX - Title

- ID: DEC-XXX
- Type: Decision
- Origin:
- Parent:
- Area:
- Priority:
- Status: Proposed
- Owner:
- Reviewer:
- Dependencies:
- Decision:
- Why:
- Outcome:
- Follow-up:
```

```md
### ACT-XXX - Title

- ID: ACT-XXX
- Type: Action
- Origin:
- Parent:
- Area:
- Audit scope:
- Priority:
- Status: Proposed
- Owner:
- Reviewer:
- Dependencies:
- Summary:
- Why it matters:
- Next check:
- Closure:
- Remaining:
- Follow-up:
```

## Current Snapshot

- Current focus: [short summary]
- Main architectural direction: [short summary]
- Main product direction: [short summary]

## Live Records

[Add active IDE / DEC / ACT records here.]

## Audit Queue

[Add recurring audit actions here.]
