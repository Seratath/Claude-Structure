# Agent Registry

> The PM reads this to know what agents are available. Never dispatch an agent not listed here. If new work requires a new agent, add it here before dispatching.

---

## Infrastructure Agents

These agents are immune to retrospective — they only change on explicit user instruction.

| Agent | File | Purpose | Capability required |
|---|---|---|---|
| PM | (the orchestrating model itself) | Orchestrates pipeline, gates approvals, maintains state | Large/capable model — needs context awareness and tool use |
| QC | `agents/qc-agent.md` | Validates agent output at each gate | Can run on limited-context model |
| Logger | `agents/logger-agent.md` | Writes approved actions to tasks/ files | Can run on limited-context model |
| Repo Manager | `agents/repo-manager.md` | Checks and maintains local + remote repo state | Needs git tool access |

---

## Pipeline Agents

These agents do the work. Eligible for retrospective improvement.

| Agent | File | Purpose | Input | Output |
|---|---|---|---|---|
| Prompt Agent | `agents/prompt-agent.md` | Improves user prompt — fills gaps, clarifies intent | `input.md` with raw user request | `output.md` with improved prompt |
| Planning Agent | `agents/planning-agent.md` | Builds high-level plan (plan mode) or step breakdown (step mode) | `input.md` with approved prompt + mode flag | `output.md` with plan or step list |
| Retrospective Agent | `agents/retrospective-agent.md` | Analyses agent failures, proposes agent profile amendments | `input.md` with failure context + agent profile | `output.md` with proposed amendment diff |

---

## Strategic Agents

Invoked at milestones, not within the pipeline.

| Agent | File | Purpose | When invoked |
|---|---|---|---|
| GA | `agents/ga.md` | North Star owner — owns goals.md, challenges drift | Milestone completion, direction changes, periodic alignment checks |

---

## Input / Output Contracts

All pipeline and infrastructure agents follow the artifact schema defined in `protocol/artifact-schema.md`.

Every agent receives `work/[job-id]/input.md` and writes to:
- `work/[job-id]/output.md`
- `work/[job-id]/status.json`
- `work/[job-id]/trace.md`

Strategic agents (GA) do not use the work/ directory — they read and write directly to `tasks/`.

---

## Project-Specific Agents

Execution agents handle Stage 4 (actual delivery). The template provides `agents/execution-agent.md` as the base — copy it, rename it, and fill in the Project-Specific Context section at bootstrap.

| Agent | File | Purpose | Input | Output |
|---|---|---|---|---|
| Execution Agent (base) | `agents/execution-agent.md` | Base template — produces complete file content from a step brief | `input.md` with step brief + file paths | `output.md` with complete, ready-to-apply file content |
| *(project copy)* | `agents/[domain]-agent.md` | Specialised for this project's language/framework | Same | Same |

**Key constraint:** execution agent output is always complete file content — never a description of what to write, never partial content. See `agents/execution-agent.md` for the full posture.

Check `Sources/Claude-Structure/Agents/` for existing profiles before building from scratch. Project-specific agents are eligible for retrospective improvement.

---

## Adding a New Agent

1. Check `Sources/Claude-Structure/Agents/` for an existing profile to adapt
2. Create the profile in `agents/[name].md` using the agent profile structure
3. Add it to this index with its input/output contract and retrospective eligibility
4. Note the addition in `tasks/decisions.md` with reason
5. If it is a pipeline agent: add it to the dispatch table in `CLAUDE.md` (or the relevant model adapter)
