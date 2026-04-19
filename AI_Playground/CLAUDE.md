# AI Playground

> This is a structured, repo-backed workspace. Every project is an independent git repository with its own CLAUDE.md, task tracking, and agent profiles. Work happens inside projects, not at the root. This file is the routing layer — it tells you where to go and how to get started, not how to do the work.

## Workspace Structure

```
AI_Playground/
  CLAUDE.md          -- you are here (workspace orchestrator)
  Projects/          -- independent project repos (each with own CLAUDE.md)
  MCP/               -- MCP server repos (infrastructure, not projects) [future]
```

## Projects (`Projects/`)

Each project is a self-contained git repo. New projects are bootstrapped from the `lifecycle-engineering` template (or another template of your choice).

| Project | Directory | Description |
|---------|-----------|-------------|

## MCP Servers (`MCP/`) — Future

MCP servers are infrastructure, not projects. They have their own repos and deployment pipelines. Do not apply project workflow rules to them. This section is reserved for plugins and MCP servers added later.

| Server | Directory | Description |
|--------|-----------|-------------|

## Routing Rules

**When invoked at the workspace root:**

1. Identify which project the user's request relates to
2. If it maps to a project: read that project's `CLAUDE.md` and follow its workflow entirely — this root file no longer applies
3. If it maps to an MCP server: work within that server's repo
4. If it's ambiguous: ask the user which project before proceeding
5. **Never blend contexts** — do not read files from one project while working in another unless the user explicitly requests it

## Project Isolation

- Each project has its own git history, CLAUDE.md, agents, tasks, and decisions
- Do not carry context, memories, or conventions between projects — domain drift is a critical risk
- If you need information from another project, ask the user first
- MCP servers are shared infrastructure — changes to them may affect multiple projects

## Starting a New Project

Clone or copy the `lifecycle-engineering` template into a new directory under `Projects/`, then:

1. Create a new repo on GitHub and clone it into `Projects/<new-project>/`
2. Copy the template structure into the new project root (everything except `.git/`)
3. Fill in the placeholder values in `CLAUDE.md` (project name, repo URL, product, stack)
4. The project's bootstrap check will prompt for any remaining gaps on first session
5. Commit the initial structure and push to GitHub
6. Add the new project to the table above

### What the template provides

- `CLAUDE.md` — project workflow, git rules, agent dispatch, task management
- `agents/` — composable agent profiles that grow with the project
- `tasks/` — goals, workboard, decisions, lessons
- `docs/plans/` — persistent plan documents
- `repos/` — cloned source repos for analysis (gitignored)
- `diagrams/` — Mermaid diagrams

## Session Anchor (Compression-Resilient)

**On every session at the workspace root:**

1. Read this file — re-establish workspace layout and routing rules
2. Identify the target project before doing any work
3. Route into the project and follow its CLAUDE.md from that point
4. **Never work across project boundaries without explicit user direction**

*This block survives context compression. When in doubt about workspace state, re-read this file.*

## Workspace Hygiene

- Keep the project table above current — update it when projects are added or removed
- Projects that are archived or abandoned should be noted in the table, not silently left
- Git remotes use GitHub — HTTPS or SSH both acceptable
- This file should stay concise — it's a router, not a manual
