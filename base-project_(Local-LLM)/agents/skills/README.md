# Skills

Skills are reusable procedures that agents follow for specific tasks. They encode **how** to do something, complementing agent profiles which encode **who** the agent is and **what** they check.

## How Skills Work

1. Each skill file defines a repeatable procedure for a specific task type
2. Agent profiles list their associated skills in the `## Skills` section
3. The PM (or the agent itself) reads the relevant skill file when the task matches
4. Skills are only loaded when needed — not on every dispatch

## Skills and the Artifact Schema

Skills that produce deliverables must follow the artifact schema in `protocol/artifact-schema.md`. Specifically:

- The skill's **Output Format** section must map to `work/[job-id]/output.md`
- The skill's **Quality Checks** section defines the PASS criteria that QC will verify
- If the skill has internal steps, the agent should update `status.json` at each step

Skills that are purely analytical (no file output) do not need to follow the artifact schema.

## Creating a New Skill

Copy `_TEMPLATE.md` and fill in the sections. Keep skills focused — one procedure per file.

Skills that are generic enough to work across projects should be contributed back to `Sources/Claude-Structure/` so other projects can use them.

## Skill vs Agent

- **Skill:** a procedure an existing agent follows for a specific task type
- **Agent:** a persistent role with its own identity, posture, and domain ownership

If the same type of work recurs but doesn't need a separate identity or domain perspective, write a skill. If it needs its own judgment, posture, and long-term ownership, write an agent.
