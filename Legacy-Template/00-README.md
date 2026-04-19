# Project Docs Structure

This repo uses a small numbered documentation set so humans and AI collaborators can find the right source of truth quickly and keep it in sync with low overhead.

## Core Docs

### `00-README.md`

This file. Explains the structure and where information belongs.

### `01-COLLABORATION-AND-ENGAGEMENT.md`

How work should be coordinated across humans and AI:

- claiming work
- ownership rules
- escalation rules
- review expectations
- documentation sync expectations

### `02-GOAL-AND-PRINCIPLES.md`

The stable north star for the project:

- what is being built
- why it should feel the way it does
- core product and design principles
- constraints and non-goals

### `03-DESIGN-AND-REQUIREMENT.md`

The reference for project-specific system behavior and requirements:

- formulas
- scaling models
- caps
- functional constraints
- runtime or state rules

### `04-WORKBOARD.md`

The operational source of truth for execution.

Use it for:

- ideas
- decisions
- actions
- ownership and reviewers
- dependencies and sequencing
- closure notes and audit findings

### `05-CHANGELOG.md`

Historical event log for deliveries, redirects, abandoned work, audits, and notable changes once they are no longer active workboard state.

## Working Rules

- Keep collaboration rules in `01`, stable intent in `02`, project-specific requirements in `03`, active work in `04`, and historical events in `05`.
- Prefer updating one clear source rather than duplicating the same information across files.
- If an item is only partially implemented, say so explicitly.
- If work stops, shifts, or is superseded, close or re-state the affected workboard item before starting the next item unless explicitly told not to.

## Hard Rules

- No new meaningful work without a record in the workboard.
- No context switch without a closure or handoff note unless explicitly told to skip it.
- No audit without either a clear "no drift found" closeout or spawned follow-up records.

## Record Model

The workboard uses three core record types:

- `IDE`: idea or concept
- `DEC`: decision
- `ACT`: action

Every meaningful record should carry:

- `ID`
- `Origin`
- `Parent`

Lineage rules:

- `Origin` is the first source in the chain.
- `Parent` is the immediate previous step.
- Root items use themselves as `Origin` and `none` as `Parent`.
- Spawned items inherit `Origin` and set `Parent` to the immediate source.

## Labels

Core shared fields:

- `Priority`: `Must`, `Should`, `Nice`
- `Owner`
- `Reviewer`
- `Dependencies`

Recommended tags:

- `Area`: project-specific, but keep it short and controlled
- `Audit scope`: `Runtime`, `Docs`, `UX`, `Tests`, `Persistence` or project equivalents

Keep the vocabulary small. If a label is not clearly earning its keep, do not add it.

## Template Examples

### `02-GOAL-AND-PRINCIPLES.md` Example

```md
# Project Name - Goal and Principles

## Project Goal

Build a lightweight internal reporting tool that lets non-technical staff generate, filter, and export team performance summaries without requiring developer involvement.

## Product North Star

The tool should feel:

- fast and self-explanatory for first-time users
- reliable and consistent across all supported data sources
- low-friction for recurring weekly and monthly workflows

## Core Experience Principles

### 1. Clarity over completeness

- Show only the data the current user role needs.
- Do not expose configuration options irrelevant to standard workflows.

### 2. Predictable output

- Exports should match what is displayed on screen.
- Users should not need to reformat output after downloading.

## Current Directional Constraints

- The report view should remain the primary working surface.
- Filtering must not require a page reload.

## Current Non-Goals

- Real-time data streaming
- Custom dashboard builder
- Public-facing reporting endpoints
```

### `03-DESIGN-AND-REQUIREMENT.md` Example

```md
# Project Name - Design and Requirement

## Key Formulas and Models

### Score aggregation

Score(item) = sum(weighted_values) / total_weight

### Pagination

PageCount = ceil(total_records / page_size)

## Current System Rules

### Data access

- read-only users may not trigger exports over 10,000 rows
- filters are applied before any aggregation

### Constraint rules

- session tokens expire after 30 minutes of inactivity
- date range filters cannot span more than 12 months
- export file size is capped at a defined maximum

## Known Watchpoints

- large date ranges may cause slow query times
- aggregation must not be affected by null values in optional fields
```

Rule of thumb:

- if it explains why the project exists or what good feels like, it belongs in `02`
- if it explains what the system must do or how it currently behaves, it belongs in `03`

### `05-CHANGELOG.md` Example

```md
## 2026-04-05

### Designed - IDE-004
- Origin: IDE-004
- Parent: none
- What: Captured a concept for a role-based export permission model.
- Why: Unrestricted exports were causing performance issues for large datasets.

### Decided - DEC-002
- Origin: IDE-004
- Parent: IDE-004
- What: Agreed that export caps should apply only to read-only roles.
- Why: Power users need unrestricted access for bulk reporting.

### Delivered - ACT-019
- Origin: IDE-004
- Parent: DEC-002
- What: Implemented export cap and role check on the export endpoint.
- Why: Put the agreed access model into the runtime.
```
