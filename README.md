# Claude Structure

Most people use Claude Code like a chatbot that can edit files. This gives it structure — a workspace where every project is independent, git-backed, and built to support multiple people and agents working in parallel without getting in each other's way.

You get source-controlled projects with persistent memory, clean isolation, and repeatable scaffolding. Claude reads the project state at the start of every session — goals, active work, decisions, lessons — so nobody has to re-explain context, whether it's you picking up tomorrow or a colleague picking up for the first time.

Clone this repo, drop the folders into place, and you're ready to start your first project.

## Get Started

1. Clone this repo somewhere on your machine
2. Copy `AI_Playground/` to where you want your workspace root (rename it if you like)
3. Copy your chosen project template (e.g. `lifecycle-engineering/`) into your workspace's projects folder
4. Open Claude Code at the workspace root — it will read `CLAUDE.md` and walk you through the rest

## What You Get

**Projects that don't interfere with each other** — every project is its own git repo with its own instructions, agents, and history. Work across multiple projects in parallel without any of them contaminating each other.

**Sessions that pick up where you left off** — goals, active work, decisions and their rationale, lessons from mistakes — all tracked in the project, not in your head. Claude reads the state at session start. You direct work, not re-explain it.

**Repeatable scaffolding** — templates give every new project a clean, consistent starting point. Same structure, same standards, every time. No "how did we set up the last one" archaeology.

**Agents that fit the work** — templates ship with agent profiles tailored to the domain. The default `lifecycle-engineering` template comes with six specialist roles (SRE, DEV, DBE, QA, SEC, GA) that run deep dives, round-table reviews, and adversarial challenges. Other templates can define entirely different teams.

## What's In Here

| Directory | What it gives you |
|-----------|------------------|
| `AI_Playground/` | Workspace orchestrator — routes Claude to the right project, enforces isolation, handles bootstrapping new projects from templates |
| `base-project/` | Generic project template — starts with GA (North Star guardian) only, grows its agent team as the work demands it. Good for any domain. Start here if unsure. |
| `lifecycle-engineering/` | SaaS/platform engineering template — six specialist agents (SRE, DEV, DBE, QA, SEC, GA) for mature platform work. Use when the domain is known and the team shape is clear. |
| `Agents/` | Shared agent library — copy profiles into your project as needed. Organised by domain (generic, saas, game). Add new ones as they emerge. |
| `Skills/` | Shared skills library — reusable procedures injected into agent dispatches for specific repeatable task types. |

## Which Template?

**Not sure where to start?** Use `base-project/`. It opens with a short GA-led conversation to capture your vision, then gets out of the way. Agents and structure grow from the work.

**Know your domain and team shape?** Use a specialist template like `lifecycle-engineering/` for a pre-built agent team suited to that type of work.

**Building something new that doesn't fit existing templates?** Start with `base-project/`, build the agents you need, then contribute the good ones back to `Agents/`.

## How It Works

The workspace has two layers:

**Workspace root** (`AI_Playground/CLAUDE.md`) — Claude reads this first. It knows where all your projects live, routes to the right one, and enforces isolation between them. It's a router, not a manual.

**Project root** (`<project>/CLAUDE.md`) — once routed, Claude follows the project's own instructions entirely. Git workflow, agent dispatch, task tracking, and standards all live here. The workspace layer steps aside.

## Adding a New Project

1. Create a new repo on GitHub
2. Clone it into your projects folder
3. Copy a template into it (everything except `.git/`)
4. Fill in the placeholders in `CLAUDE.md`
5. Open Claude at the project root — it will prompt for anything still missing
6. Add the project to the workspace table

## Philosophy

- Work happens in projects, not at the workspace root
- Every project is isolated — no context bleeds between them
- All output is committed — nothing lives only in chat history
- Templates are the floor, not the ceiling — enrich them as projects grow
