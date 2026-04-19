# [Project Name]

> This is a repo-backed project. All meaningful work produces versioned artifacts committed via git. This file is the project's operating instructions — read it at the start of every session.

## Project Identity

**What we're building:** [Populated by GA at session 1]
**Why it exists:** [Populated by GA at session 1]
**Repo:** [REPO_URL]

## Bootstrap — First Session Only

If this file still contains placeholder text above, the project hasn't been bootstrapped yet.

**Do this before any other work:**

1. Invoke GA: read `agents/ga.md` and conduct the North Star interview
2. GA commits the completed `tasks/goals.md`
3. Return here, fill in Project Identity above, and commit
4. Start work

The interview takes one short conversation. Rough answers are fine — goals.md evolves. The point is to have *something* committed before the first task, not to have it perfect.

## Git Workflow

This repo lives at [REPO_URL]. Main is protected.

All changes go through pull requests:

1. **Branch** from main with a descriptive name
2. **Commit** with clear messages explaining what and why
3. **Push** and open a PR: `git push -u origin <branch>` then `gh pr create --title "..." --body "..."`
4. **User merges** via GitHub UI — Claude cannot merge
5. **Pull** after merge: `git pull origin main && git fetch --prune`

**Working directory safety:** Before any git operation, verify you are in the project root — not inside a cloned repo under `repos/`. Run `git rev-parse --show-toplevel` to confirm.

**Git conventions:**
- Claude handles all git operations (branch, commit, push, PR creation)
- Commit messages include `Co-Authored-By: <Model & Version> <noreply@anthropic.com>`
- Branches are short-lived and focused
- Delete source branch on merge

## Agent Team

This project starts with GA only. Agents are added when work demands them — not upfront.

| Shorthand | Profile | Model | Status |
|-----------|---------|-------|--------|
| GA | agents/ga.md | sonnet / opus | Active — North Star owner |

**When to add an agent:** When a domain concern keeps arising that the orchestrator isn't equipped to analyse deeply, or when the same type of specialist work is recurring. Check `Agents/` in the Claude-Structure repo first — copy the closest match and adapt it. If nothing fits, build one from scratch using the agent profile structure.

**When not to add an agent:** When a skill would do. If it's a repeatable procedure rather than a persistent domain perspective, write a skill instead.

### Dispatch Protocol

To invoke any agent: read `agents/team-charter.md` (if it exists) + `agents/standards.md` (if it exists) + the agent's profile → compose a prompt with the agent's identity, relevant project context, and the task → launch via the Agent tool → report findings attributed to the role.

GA is invoked at milestones, direction changes, and periodic alignment checks — not for routine tasks. All other agents are invoked on demand.

## Workflow Orchestration

### 1. Project Isolation

Each project is independent. Do not carry context, memories, or conventions from other projects unless the user explicitly instructs it.

### 2. Plan Before Building

For any task with 3+ steps or an architectural decision: enter plan mode first. Write the plan to `docs/plans/` — not ephemeral notes. Plans that are fully executed or superseded should be removed.

### 3. Build What's Needed

Don't add features, agents, or structure beyond what the current work requires. The project grows by doing, not by anticipating. When something new is genuinely needed, add it — then note it.

### 4. Decisions Accumulate

Every non-obvious decision goes in `tasks/decisions.md`. This is how the project builds traditional clarity over time — not by planning everything upfront, but by recording what was decided and why as it happens.

### 5. Learn From Mistakes

After any correction: update `tasks/lessons.md` with the pattern and a rule to prevent recurrence. Review lessons at session start.

### 6. Verify Before Done

Never mark a task complete without proving it works. Ask: "Would the person who defined this goal consider this done?"

### 7. Subagents

Use subagents to keep the main context clean. Offload research, exploration, and parallel analysis. One focused task per subagent.

## Source Repositories

Repos cloned for analysis go in `repos/`. Every cloned repo must be recorded in `repos/SOURCES.md` with its URL, branch/commit, and purpose. The `repos/.gitignore` excludes all repo content — only `SOURCES.md` and `.gitignore` are tracked.

## Diagrams

Mermaid syntax, saved as `.md` files in `diagrams/`. Validate syntax before committing.

## Task Management

| File | Purpose | Update Frequency |
|------|---------|-----------------|
| `tasks/goals.md` | North Star — what we're building, why, principles, non-goals | When direction changes (GA owns this) |
| `tasks/workboard.md` | Active work — status, next steps, closure notes | Every session |
| `tasks/decisions.md` | Decision log — what was decided, why, when | When decisions are made |
| `tasks/lessons.md` | Mistake patterns and rules | After corrections |

## Session Anchor (Compression-Resilient)

**Before starting ANY task:**

1. `git pull origin main` — sync with remote
2. `git status` — confirm clean working tree on main
3. Read `tasks/goals.md` — re-establish the North Star
4. Read `tasks/workboard.md` — understand current state
5. Read `tasks/lessons.md` — review rules to prevent known mistakes
6. **Bootstrap check** — if Project Identity above still contains placeholders, stop and run the bootstrap before proceeding

This block survives context compression. Always re-read at task boundaries — do not assume prior reads are still in context.

## Closure Discipline

Before context-switching away from active work:

- Update workboard with current status and remaining work
- If complete: one-line closure note
- If abandoned or deferred: say why
- If a decision was made: add it to `decisions.md`

## Core Principles

- **Vision before plan** — capture the why first, let the how emerge from the work
- **Clarity by accumulation** — decisions, lessons, and agent context build up as the project progresses; they aren't demanded upfront
- **Fit the tool to the work** — add agents and skills when the work needs them, not before
- **Commit everything meaningful** — nothing important lives only in conversation history
- **GA owns the compass** — when direction feels uncertain, invoke GA before pushing further
