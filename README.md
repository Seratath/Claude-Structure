# Claude Structure

Most people use Claude Code like a chatbot that can edit files. This project is designed to give it structure — a workspace where every project is independent, git-backed, and built to support multiple people and agents working in parallel without getting in each other's way.

You get source-controlled projects with persistent memory, clean isolation, and repeatable scaffolding. Claude reads the project state at the start of every session — goals, active work, decisions, lessons — so nobody has to re-explain context, whether it's you picking up tomorrow or a colleague picking up for the first time.

## Get Started

Open Claude Code in the directory you want as your workspace root. Tell it:

> Set me up using this structure: https://github.com/Seratath/Claude-Structure

Claude will check the directory, confirm with you before doing anything, clone the structure, install the workspace orchestrator, and ask what you'd like to start with. That's it — no manual copying, no template archaeology.

Subsequent sessions: just open Claude at the workspace root. It reads the orchestrator, checks nothing's broken, and picks up where you left off.

## Claude Bootstrap — Setup Procedure

> This section is instructions *for Claude* when a user asks to be set up from this URL. Follow it defensively: ask before destroying, explain before acting on anything unusual. Every step is idempotent — re-running produces the same state, not duplicates.

### 1. Check the directory

- Run `pwd` to confirm the absolute path. Tell the user where they are.
- List the directory contents. If it has unrelated files, warn the user and ask whether to set up here or pick another location.
- If `./CLAUDE.md` already exists, show the user its first few lines and ask before overwriting.
- If the current path contains `Sources/Claude-Structure/` (check with `pwd`), warn the user they may be nesting a workspace inside a template source. Ask whether they meant to run Claude from the workspace root instead.
- Confirm explicitly: **"Set up AI Playground workspace here: `<absolute path>`. Proceed?"** Wait for confirmation.

### 2. Clone the template source

- If `Sources/Claude-Structure/` already exists with a `.git` directory, skip this step (tell the user it's already there).
- Otherwise: `git clone https://github.com/Seratath/Claude-Structure Sources/Claude-Structure`

### 3. Install the workspace orchestrator

- If `./CLAUDE.md` exists and the user approved overwrite in step 1, back it up to `./CLAUDE.md.backup-<timestamp>` first.
- Copy `Sources/Claude-Structure/AI_Playground/CLAUDE.md` to `./CLAUDE.md`.

### 4. Create workspace folders

- If `Projects/` doesn't exist, create it by copying `Sources/Claude-Structure/AI_Playground/Projects/` (preserves the README placeholder so the folder isn't empty).

### 5. Install .gitignore

- If `./.gitignore` doesn't exist, copy `Sources/Claude-Structure/AI_Playground/.gitignore` to `./.gitignore`.
- If it exists, show the user and ask whether to merge or leave alone.

### 6. Hand off

- Read the newly-installed `./CLAUDE.md` and follow its routing rules from that point.
- Tell the user what was done (or confirm nothing changed if everything was already in place).
- Ask what they'd like to start with — a new project, or just exploring the structure.

## What You Get

**Projects that don't interfere with each other** — every project is its own git repo with its own instructions, agents, and history. Work across multiple projects in parallel without any of them contaminating each other.

**Sessions that pick up where you left off** — goals, active work, decisions and their rationale, lessons from mistakes — all tracked in the project, not in your head. Claude reads the state at session start. You direct work, not re-explain it.

**Repeatable scaffolding** — templates give every new project a clean, consistent starting point. Same structure, same standards, every time. No "how did we set up the last one" archaeology.

**Agents that fit the work** — templates ship with agent profiles tailored to the domain. `lifecycle-engineering` comes with six specialist roles (SRE, DEV, DBE, QA, SEC, GA). `base-project` starts minimal and grows. Other templates can define entirely different teams.

## What's In Here

| Directory | What it gives you |
|-----------|------------------|
| `AI_Playground/` | Workspace template — orchestrator CLAUDE.md, folder skeleton, .gitignore, placeholder READMEs |
| `base-project/` | Generic project template — starts with GA only, grows its agent team as work demands. Good for any domain. Start here if unsure. |
| `lifecycle-engineering/` | SaaS/platform engineering template — six specialist agents for mature platform work. Use when the domain is known. |
| `Agents/` | Shared agent library — copy profiles into your project as needed. Organised by domain (generic, saas, game). |
| `Skills/` | Shared skills library — reusable procedures injected into agent dispatches for specific repeatable task types. |
| `Legacy-Template/` | The original numbered-docs template, preserved for reference and migration. Don't use for new projects. |

## Which Template?

**Not sure where to start?** Use `base-project/`. It opens with a short GA-led conversation to capture your vision, then gets out of the way. Agents and structure grow from the work.

**Know your domain and team shape?** Use a specialist template like `lifecycle-engineering/` for a pre-built agent team suited to that type of work.

**Building something new that doesn't fit existing templates?** Start with `base-project/`, build the agents you need, then contribute the good ones back to `Agents/`.

## How It Works

The workspace has two layers:

**Workspace root** (`<workspace>/CLAUDE.md`) — Claude reads this first. It knows where all your projects live, routes to the right one, and enforces isolation between them. It's a router, not a manual.

**Project root** (`<workspace>/Projects/<project>/CLAUDE.md`) — once routed, Claude follows the project's own instructions entirely. Git workflow, agent dispatch, task tracking, and standards all live here. The workspace layer steps aside.

`Sources/Claude-Structure/` lives in the workspace as a live clone of this repo. Templates, shared agents, and shared skills are always available to the orchestrator without manual copying. `git pull` in there to get updates.

## Philosophy

- Work happens in projects, not at the workspace root
- Every project is isolated — no context bleeds between them
- All output is committed — nothing lives only in chat history
- Templates are the floor, not the ceiling — enrich them as projects grow
- The setup experience is architected, not improvised — users share a URL, not a procedure
