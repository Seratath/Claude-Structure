# Projects

Each subdirectory here is an independent git repository — a self-contained project with its own `CLAUDE.md`, agents, tasks, and history.

## Starting a new project

Ask the workspace orchestrator (the Claude session at the workspace root) to start a new project. It'll walk you through:

1. Project name and optional GitHub repo
2. Template choice (`base-project/` unless the domain clearly fits a specialist template)
3. Scaffolding and initial commit

The orchestrator reads templates from `Sources/Claude-Structure/` — you don't copy anything manually.

## Rules

- **One project per directory.** Never mix project contexts.
- **Each project is its own git repo.** The workspace itself may or may not be tracked in git; project-level commits are what matter.
- **Don't work across projects without explicit direction.** Orchestrator rules enforce isolation.
