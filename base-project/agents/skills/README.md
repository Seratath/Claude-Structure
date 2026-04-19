# Skills

Skills are reusable procedures that agents follow for specific tasks. They encode **how** to do something, complementing the agent profiles which encode **who** the agent is and **what** they check.

## How Skills Work

1. Each skill file defines a repeatable procedure for a specific type of work
2. Agent profiles list their associated skills in the `## Skills` section
3. The orchestrator reads the relevant skill file when the task matches
4. Skills are only loaded when needed — not every dispatch

## Creating a New Skill

Copy `_TEMPLATE.md` and fill in the sections. Keep skills focused — one procedure per file.

Generic skills that work across projects should be merged back to the template repo.
