# Project Protocol

> Model-agnostic operating instructions. All agents and PM models read this. Model-specific adapters (CLAUDE.md, LOCAL_LLM.md) are thin wrappers that point here. This file is the canonical source of truth for how this project operates.

---

## What This Is

A structured pipeline for running project-type work with multiple LLM agents. The PM orchestrates. Agents execute. Files are the memory. No agent — including the PM — should rely on conversation history for anything structural.

---

## File Structure

```
project-root/
  protocol/
    core.md           ← this file — canonical protocol
    pm-role.md        ← PM identity, dispatch rules, fail handling
    state.md          ← live project state (rewritten each rebase)
    artifact-schema.md ← file contracts for all agent jobs
  agents/
    INDEX.md          ← registry of all agents
    ga.md             ← Growth & Alignment Analyst (North Star owner)
    prompt-agent.md
    qc-agent.md
    planning-agent.md
    retrospective-agent.md
    logger-agent.md
    repo-manager.md
    skills/           ← reusable procedures
    team-charter.md   ← shared standards
  tasks/
    goals.md          ← North Star (GA owns)
    workboard.md      ← active work
    decisions.md      ← decision log
    lessons.md        ← mistake patterns and rules
  work/
    [job-id]/         ← per-agent job directories (see artifact-schema.md)
    archive/          ← completed job directories post-rebase
  docs/plans/         ← persistent plan documents
  diagrams/           ← Mermaid diagrams
  repos/              ← cloned source repos for analysis (gitignored)
  CLAUDE.md           ← Claude adapter (points here)
  LOCAL_LLM.md        ← Local LLM adapter (system prompt content)
```

---

## Pipeline Stages

### Stage 0: Threshold Check
PM decides: full pipeline or direct answer. See `protocol/pm-role.md` for criteria.

### Stage 1: Prompt Improvement
*Purpose: fill gaps and clarify intent before any planning work begins.*

User input → **Prompt Agent** → **QC** → PM surfaces to user → **Approval**

### Stage 2: High-Level Planning
*Purpose: delivery-criteria-focused plan. Not implementation detail.*

Approved prompt → **Planning Agent** → **QC** → PM → **Approval**

### Stage 3: Step Breakdown
*Purpose: procedural steps small enough to be executed by limited-context models.*

Each plan item → **Planning Agent (step mode)** → **QC** → PM → **Approval**

### Stage 4: Execution Loop
*Purpose: deliver each step.*

Each step → appropriate agent → **QC** → PM → **Approval**

Repeat until all steps complete.

### Cross-cutting (non-blocking, post-approval)
- **Logger Agent** — fires after every approval, writes to tasks/
- **Repo Manager** — fires after each pipeline cycle, checks local and remote state

---

## Approval Gates

Every stage requires explicit user approval before the pipeline advances.

The PM surfaces: what was produced, what comes next, any QC flags.

User options at every gate:
- **Approve** — advance
- **Reject + feedback** — re-run same stage with clarified input
- **Stop** — halt and update workboard
- **Change direction** — re-enter pipeline at appropriate stage

A rejection is not a failure. "No, I meant X" re-runs the agent — it does not trigger retrospective.

---

## Fail / Retry Rules

**On FAIL:**
1. Environmental failure (timeout, tool error, missing file) → retry once with same input
2. Second failure or non-environmental → surface to user with trace summary
3. User decides: retry with changes / stop / change direction
4. Log issue type to state.md retrospective queue

**On BLOCKED:**
1. PM reads trace.md, identifies specific blocker
2. Surfaces blocker to user with precise description
3. Resolves blocker, re-dispatches

Never retry silently more than once.

---

## Retrospective Trigger Rules

The Retrospective Agent is only eligible when:
- Same agent produces 2+ rejections of the same type in a session
- User explicitly directs: "make [agent] better at X"

**Infrastructure agents (PM, QC, Logger, Repo Manager) are immune** — they only change on explicit user instruction.

A single rejection, a changed direction, or an environmental failure does not trigger retrospective.

---

## Context Rebase

After 1-2 complete pipeline cycles, or when context is fragmented:
1. Write current state to `protocol/state.md`
2. Write open items to `tasks/workboard.md`
3. Compact the session to a 3-5 bullet summary in state.md
4. Resume from files — treat the next turn as a fresh session

---

## GA and the North Star

GA (Growth & Alignment Analyst) owns `tasks/goals.md`. GA is not a pipeline agent — it is invoked by the PM at milestone boundaries, direction changes, and periodic alignment checks. Between those moments, GA is not in the room.

If work arises that doesn't trace back to goals.md, surface it to GA before proceeding.

---

## Git Workflow

1. Branch from main with a descriptive name
2. Commit with clear messages — what and why
3. Push and open a PR
4. User merges via UI — the PM does not merge
5. Pull after merge: `git pull origin main && git fetch --prune`

Verify working directory before any git operation: `git rev-parse --show-toplevel`

---

## Task Files

| File | Purpose | Who writes |
|---|---|---|
| `tasks/goals.md` | North Star | GA |
| `tasks/workboard.md` | Active work, status, next steps | Logger Agent + PM |
| `tasks/decisions.md` | Non-obvious decisions, why, alternatives | Logger Agent |
| `tasks/lessons.md` | Mistake patterns and amendment rules | Logger Agent + Retrospective Agent |

---

## Session Anchor

Before starting any task, read in order:
1. `protocol/state.md` — re-establish current state
2. `tasks/goals.md` — re-establish North Star
3. `tasks/workboard.md` — understand active work
4. `tasks/lessons.md` — apply known rules

If project identity placeholders remain in this file or goals.md: run the GA bootstrap interview before any other work.

*This checklist is compression-resilient. Re-run it whenever state feels uncertain — do not assume prior reads are still in context.*

---

## Project Identity

**What we're building:** [Populated at session 1 via GA bootstrap]
**Why it exists:** [Populated at session 1 via GA bootstrap]
**Repo:** [REPO_URL]
