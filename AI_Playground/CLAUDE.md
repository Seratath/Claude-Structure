# AI Playground

> This is a structured, repo-backed workspace. Every project is an independent git repository with its own CLAUDE.md, task tracking, and agent profiles. Work happens inside projects, not at the root. This file is the routing layer — it tells you where to go and how to get started, not how to do the work.

## Bootstrap Check (run every session)

Before any other work, verify the workspace is intact:

1. **`Sources/Claude-Structure/` must exist** — it provides the template sources for new projects and any future updates to this orchestrator.
   - If missing: **do not auto-restore.** Tell the user it's missing, explain what it's for, and ask before re-cloning from `https://github.com/Seratath/Claude-Structure` into `Sources/Claude-Structure/`. Respect their answer.

2. **`Projects/` must exist** — this is where individual project repos live.
   - If missing: create it silently with a placeholder README from `Sources/Claude-Structure/AI_Playground/Projects/README.md` if available, otherwise an empty folder.

If both exist, proceed to normal routing below without comment. This check is idempotent — it does nothing when everything is in place.

## Workspace Structure

```
<workspace root>/
  CLAUDE.md          -- you are here (workspace orchestrator)
  Projects/          -- independent project repos (each with own CLAUDE.md)
  Sources/
    Claude-Structure/   -- live clone of structure repo (templates, shared agents, skills)
  MCP/               -- MCP server repos (infrastructure, not projects) [future]
```

## Projects (`Projects/`)

Each project is a self-contained git repo. New projects scaffold from `Sources/Claude-Structure/base-project/` (default) or another template.

| Project | Directory | Description |
|---------|-----------|-------------|

## MCP Servers (`MCP/`) — Future

MCP servers are infrastructure, not projects. They have their own repos and deployment pipelines. Do not apply project workflow rules to them. Reserved for plugins and MCP servers added later.

| Server | Directory | Description |
|--------|-----------|-------------|

## Routing Rules

**When invoked at the workspace root:**

1. Run the Bootstrap Check above
2. Identify which project the user's request relates to
3. If it maps to a project: read that project's `CLAUDE.md` and follow its workflow entirely — this root file no longer applies
4. If it maps to an MCP server: work within that server's repo
5. If it's ambiguous: ask the user which project before proceeding
6. **Never blend contexts** — do not read files from one project while working in another unless the user explicitly requests it

## Project Isolation

- Each project has its own git history, CLAUDE.md, agents, tasks, and decisions
- Do not carry context, memories, or conventions between projects — domain drift is a critical risk
- If you need information from another project, ask the user first
- MCP servers are shared infrastructure — changes to them may affect multiple projects

## Starting a New Project

Templates live in `Sources/Claude-Structure/`. The flow:

1. Ask the user: name, repo URL (or offer to defer), and which template (`base-project/` unless they have a clear domain fit)
2. Create `Projects/<new-project>/` and copy the chosen template into it (everything except `.git/`)
3. If the user provided a GitHub URL, clone into the new directory first, then copy template files over
4. Fill in placeholder values in the project's `CLAUDE.md` (project name, repo URL, identity)
5. The project's own bootstrap check handles anything still missing on first session
6. Commit the initial structure and push
7. Add the project to the table above

### What the base project template provides

- `CLAUDE.md` — project workflow, git rules, agent dispatch, task management
- `agents/` — composable agent profiles (starts with GA only; grows with the work)
- `tasks/` — goals, workboard, decisions, lessons
- `docs/plans/` — persistent plan documents

### Pulling in a shared agent

Agents live in `Sources/Claude-Structure/Agents/`. When a project needs one:

1. Read `Sources/Claude-Structure/Agents/INDEX.md` to find the right profile
2. Copy the profile file into the project's `agents/` directory
3. Enrich its Project-Specific Context section for the new project
4. Add the agent to the project's dispatch table

## Session Anchor (Compression-Resilient)

**On every session at the workspace root:**

1. Read this file — re-establish workspace layout and routing rules
2. Run the Bootstrap Check
3. Identify the target project before doing any work
4. Route into the project and follow its CLAUDE.md from that point
5. **Never work across project boundaries without explicit user direction**

*This block survives context compression. When in doubt about workspace state, re-read this file.*

## Workspace Hygiene

- Keep the project table above current — update it when projects are added or removed
- Projects that are archived or abandoned should be noted in the table, not silently left
- Git remotes use GitHub — HTTPS or SSH both acceptable
- `Sources/Claude-Structure/` is a live clone — `git pull` there to get template/agent updates; never edit files there to customise a project (edit the project's copy instead)
- This file should stay concise — it's a router, not a manual
