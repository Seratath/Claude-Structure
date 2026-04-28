# [Project Name] — Gemini Adapter

> Gemini adapter for this project. The full project operating instructions live in `protocol/core.md`. This file covers Gemini-specific setup and notes.

## On Every Session

Before any work:

1. Read `protocol/core.md` — canonical project protocol
2. Read `protocol/pm-role.md` — your role and dispatch rules
3. Read `protocol/state.md` — current project state
4. Read `tasks/goals.md` — North Star
5. Read `tasks/workboard.md` — active work
6. Read `tasks/lessons.md` — rules to apply

**Bootstrap check:** If Project Identity in `protocol/core.md` still contains placeholders — run the GA bootstrap before any other work.

## Gemini-Specific Notes

**System instruction:** If using Gemini via AI Studio or the API, place the following in the system instruction field:

```
You are the Project Manager for this project. Before responding to anything, read:
1. protocol/state.md — current state and active jobs
2. protocol/pm-role.md — your role and dispatch rules
3. protocol/core.md — the full project protocol

Your memory is the files, not this conversation. Read protocol/state.md at the start of every turn.
```

**Context window:** Gemini models have large context windows. Still follow the context rebase protocol after 1-2 pipeline cycles — the discipline of writing state to files matters for recovery and multi-model handoffs, regardless of context capacity.

**Tool / function calling:** Gemini supports function calling. If tool use is available, Repo Manager can be dispatched directly. If not, Repo Manager must be run manually by the user or skipped, and git hygiene handled explicitly.

**Agent dispatch:** Gemini does not have a native Agent tool equivalent. Dispatch agents by running separate inference calls with the agent's `work/[job-id]/input.md` content as the user turn and the agent's profile as the system instruction.

**Model selection guidance:**

| Agent | Recommended Gemini model |
|---|---|
| PM | Gemini 2.0 Flash or Pro |
| QC, Logger, step-mode Planning | Gemini 2.0 Flash |
| Prompt Agent, plan-mode Planning | Gemini 2.0 Flash or Pro |
| Retrospective Agent | Gemini 2.0 Pro |
| GA | Gemini 2.0 Pro |

*Update this table as Gemini model versions change.*

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
