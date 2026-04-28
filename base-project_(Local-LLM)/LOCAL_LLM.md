# Local LLM Adapter

> Setup guide for using this project with local LLMs. Covers VS Code + Continue (primary path) and other UIs (fallback).

---

## VS Code + Continue (Primary Path)

This project ships with a `.continue/` directory that configures Continue at the project level. It is scoped to this project — it does not affect other projects or your global Continue config.

**Open VS Code at the project root, not the workspace root.** The `.continue/` config, slash commands, and all file paths resolve relative to the folder VS Code is opened in. Opening a parent directory (e.g. `AI_Playground/`) will break path resolution and the slash commands won't load correctly. One project = one VS Code folder open.

### What's included

| File | Purpose |
|---|---|
| `.continue/config.json` | Project-level system message + slash commands |
| `.continue/prompts/start.prompt` | `/start` — bootstrap the session |
| `.continue/prompts/state.prompt` | `/state` — quick state check |

### Session start (every session)

1. Open VS Code at the project root
2. Open the Continue chat panel
3. Type `/start` — Continue loads the prompt, which reads the six bootstrap files
4. PM confirms current phase, last stage, and next action
5. Work begins

That's it. One command.

### Slash commands available

| Command | What it does |
|---|---|
| `/start` | Bootstrap — reads all PM context files, confirms state |
| `/state` | Quick check — reads state.md, reports phase and next action |
| `/approve` | Signals approval — PM logs it and advances the pipeline |
| `/stop` | Halts pipeline — PM writes current state to files |
| `/rebase` | Forces context rebase — PM writes state, produces session summary |

### Tool use dependency

`/start` instructs the PM to read files. Whether it actually reads them depends on your model's tool use / file access configuration in Continue:

**Model has file reading tools enabled:**
The PM reads the files automatically on `/start`. Fully automatic.

**Model does not have file reading tools:**
Use `@file` mentions alongside `/start` to inject the files manually:

```
/start
@file protocol/state.md
@file protocol/pm-role.md
@file tasks/goals.md
@file tasks/workboard.md
@file tasks/lessons.md
```

This is more verbose but works with any model. After the first few sessions it becomes muscle memory.

### Context collapse recovery

If the PM starts behaving erratically (doing agent work itself, ignoring the pipeline, losing state):

1. Type `/rebase` — forces state to be written to files
2. Start a new chat session
3. Type `/start` — reconstructs from files

Nothing is lost. The project state lives in files, not the conversation.

---

## Other UIs (Open WebUI, LM Studio, Jan, Ollama)

No project-level config support. Use the system prompt block below.

### System Prompt Block

Copy this into your UI's system prompt or model configuration field:

```
You are the Project Manager for this project. Before responding to anything, read these files:

1. protocol/state.md        — your current state and active jobs
2. protocol/pm-role.md      — your role, dispatch rules, and how to handle failures
3. protocol/core.md         — the full project protocol

If those files are missing or empty, read tasks/goals.md and tasks/workboard.md to re-establish context.

You do not do the work. You dispatch agents, gate approvals, and keep the project moving. Your memory is the files — not this conversation.

Every turn: read protocol/state.md first. Always.
```

Keep this short — it is intentionally minimal so it survives context compression.

### Session start (other UIs)

At the start of each session, manually provide the bootstrap files:

```
[paste content of protocol/state.md]
[paste content of tasks/workboard.md]

Read the above. Confirm current phase and next action.
```

Or if your UI supports file attachment, attach those files directly.

---

## Capability Mapping

| Role | Claude equivalent | Minimum local capability |
|---|---|---|
| PM | sonnet/opus | 13B+ recommended — instruction following, tool use preferred |
| Prompt Agent | sonnet | 7B sufficient for clear inputs |
| Planning Agent (plan mode) | sonnet | 13B preferred |
| Planning Agent (step mode) | haiku | 3B–7B sufficient |
| QC Agent | haiku | 3B–7B sufficient |
| Logger Agent | haiku | 3B–7B sufficient |
| Repo Manager | sonnet | Requires tool/function calling support |
| Retrospective Agent | opus | 30B+ preferred — reasoning-heavy |
| GA | opus | 30B+ preferred — strategic analysis |
