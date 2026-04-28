# Artifact Schema

> Defines the file contracts all agents must honour. PM reads and writes these. Agents receive input, write output. No agent should read or write outside its assigned job directory.

## Directory Structure

```
work/
  [job-id]/
    input.md        ← PM writes before dispatch
    output.md       ← agent writes on completion
    status.json     ← agent updates throughout
    trace.md        ← agent reasoning log (written as it goes)
```

Job IDs follow the pattern `[agent-type]-[sequence]`, e.g. `prompt-001`, `qc-002`, `plan-001`.

For parallel jobs, each runs in its own directory. The PM tracks active job IDs in `protocol/state.md`.

Completed job directories are retained until the next context rebase, then archived to `work/archive/`.

---

## input.md

Written by the PM before dispatching an agent. Must be self-contained — the agent should need nothing else to do its job.

```markdown
# Job: [job-id]
**Agent:** [agent name]
**Task:** [one sentence — what this agent must produce]
**Context:** [minimal context required — goal summary, previous approved output if relevant]
**Success criteria:** [what PASS looks like — specific and checkable]
**Constraints:** [hard limits — what the agent must not do or assume]
```

---

## output.md

Written by the agent on completion. Format varies by agent type but must always include:

```markdown
# Output: [job-id]
**Status:** PASS | FAIL | BLOCKED
**Summary:** [one sentence — what was produced]

[Deliverable content]
```

---

## status.json

Updated by the agent at each internal checkpoint. PM monitors this file to detect progress and stuck states.

```json
{
  "job_id": "prompt-001",
  "agent": "prompt-agent",
  "status": "RUNNING | PASS | FAIL | BLOCKED",
  "step": 2,
  "total_steps": 4,
  "last_updated": "ISO-8601 timestamp",
  "note": "optional one-line status note"
}
```

**Status definitions:**

| Status | Meaning |
|---|---|
| `RUNNING` | Agent is actively working |
| `PASS` | Job complete, output ready for QC/PM review |
| `FAIL` | Agent could not complete the job |
| `BLOCKED` | Agent needs something it doesn't have — trace.md describes what |

If `status.json` shows `RUNNING` and has not been updated within the expected window, the PM treats this as a stuck signal and reads `trace.md` to diagnose.

---

## trace.md

The agent's working log. Written incrementally as the agent works — not a post-hoc summary. This is what the PM and QC read to diagnose stuck states, detect loops, or understand reasoning without re-running the job.

```markdown
# Trace: [job-id]

## Step 1: [step name]
[What the agent did and why — one short paragraph]

## Step 2: [step name]
[Continue...]

## Deviation note (if any)
[If the agent had to depart from the expected path, explain why here]
```

Minimum entry per step: one sentence. Enough to distinguish "working as expected" from "looping" or "going off-track".

---

## Parallel Job Namespacing

When the PM runs agents in parallel, each job gets its own directory. The PM records all active job IDs in `protocol/state.md` under `active_jobs`. QC is dispatched per job — QC for job A does not read job B's artifacts.

Dependencies between parallel jobs must be explicit in `input.md`. If job B depends on job A's output, job B is not dispatched until job A reaches `PASS`.
