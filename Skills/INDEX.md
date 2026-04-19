# Skills Library Index

Skills are consumable procedures injected into agent dispatches for specific repeatable task types. They encode **how** to do something — the agent profile encodes **who** and **what they check**.

## How to Use

1. When a task matches a skill, the orchestrator reads the skill file and folds it into the agent prompt
2. Skills are only loaded when the task matches — not on every dispatch
3. Copy skills you need into your project's `agents/skills/` folder
4. Skills that prove useful across projects should be contributed back here

## Creating a New Skill

Copy `_TEMPLATE.md`, fill in the sections, keep it focused — one procedure per file.

## Index

| Skill | File | Roles | Purpose |
|-------|------|-------|---------|
| *(none yet — library grows as skills are developed in projects)* | | | |

## Contributing Back

If a skill developed in a project is generic enough to apply elsewhere:

1. Strip any project-specific context from it
2. Add it to this library with a clear name and entry in this index
3. Note which role(s) it applies to
