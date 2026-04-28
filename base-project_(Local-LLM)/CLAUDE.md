# [Project Name] — Claude Adapter

> Claude Code adapter for this project. Loads the canonical protocol and adds Claude-specific notes. The full project operating instructions live in `protocol/core.md` — that file is the source of truth.

## On Every Session

Before any work:

1. Read `protocol/core.md` — canonical project protocol
2. Read `protocol/pm-role.md` — your role and dispatch rules
3. Read `protocol/state.md` — current project state
4. Read `tasks/goals.md` — North Star
5. Read `tasks/workboard.md` — active work
6. Read `tasks/lessons.md` — rules to apply
7. `git pull origin main` — sync with remote
8. `git status` — confirm clean working tree

**Bootstrap check:** If Project Identity in `protocol/core.md` still contains placeholders — stop and run the GA bootstrap before any other work.

## Claude-Specific Notes

**Agent dispatch:** Use the Agent tool to dispatch pipeline agents. The agent's `work/[job-id]/input.md` content is the prompt. One Agent tool call per job, unless explicitly running parallel jobs (send multiple calls in a single message).

**Parallel dispatch:** When running parallel independent jobs, send all Agent tool calls in one message. Record all job IDs in `protocol/state.md` Active Jobs before dispatching.

**Context compression:** Claude Code compresses prior messages as context fills. The session anchor above is compression-resilient — re-run it whenever state feels uncertain. `protocol/state.md` is always the recovery point.

**Model selection guidance:**

| Agent | Recommended model |
|---|---|
| PM (this conversation) | User's selected model |
| QC, Logger, step-mode Planning | haiku |
| Prompt Agent, plan-mode Planning | sonnet |
| Retrospective Agent | sonnet or opus |
| GA | opus |

**Git operations:** Claude handles all git operations. Verify working directory before any git command: `git rev-parse --show-toplevel`. All changes go through PRs — user merges via GitHub UI.

**Memory:** Project state lives in task and protocol files — not Claude's memory system. Do not duplicate project state into Claude memory.

## Bootstrap — First Session Only

If Project Identity placeholders are present in `protocol/core.md`:

1. Read `agents/ga.md` — conduct the North Star interview
2. GA commits the completed `tasks/goals.md`
3. Fill in Project Identity in `protocol/core.md` and commit
4. Start work

## Agent Dispatch Table

| Work type | Agent | Mode |
|---|---|---|
| Clarify user intent | Prompt Agent | — |
| Validate any agent output | QC Agent | — |
| Build delivery plan | Planning Agent | plan |
| Break plan item into steps | Planning Agent | step |
| Write to task files | Logger Agent | — |
| Check repo state | Repo Manager | — |
| Fix repeated agent failure | Retrospective Agent | — |
| North Star review | GA | — |

## Git Workflow

This repo lives at [REPO_URL]. Main is protected.

1. Branch from main with a descriptive name
2. Commit with clear messages — what and why. Include `Co-Authored-By: <Model> <noreply@anthropic.com>`
3. Push and open a PR: `git push -u origin <branch>` then `gh pr create`
4. User merges via GitHub UI
5. Pull after merge: `git pull origin main && git fetch --prune`
6. Delete source branch after merge

## Core Principles

- **Files are the memory** — nothing structural lives only in conversation history
- **Vision before plan** — GA captures the why first, let the how emerge from work
- **Clarity by accumulation** — decisions, lessons, and agent context build up as the project progresses
- **Commit everything meaningful** — if it matters, it's versioned
- **GA owns the compass** — when direction feels uncertain, invoke GA before pushing further
