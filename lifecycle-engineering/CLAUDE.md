# [Project Name]

> This is a repo-backed engineering project. All work produces versioned artifacts committed via git. This is not a general conversation workspace — every session should start with a git sync, read the project state, and work through branches and pull requests.

## Repository Structure

```
CLAUDE.md          -- you are here (project instructions, workflow, standards)
agents/            -- tiger team profiles (SRE, DEV, DBE, QA, SEC, GA)
  team-charter.md  -- shared mission, norms, quality bar
  standards.md     -- analysis & communication standards (shared by all roles)
  context.md       -- project quick reference for all agents
  skills/          -- reusable procedures agents follow for specific tasks
diagrams/          -- architecture and data flow diagrams (mermaid .md files)
docs/              -- analysis and investigation documents
  plans/           -- implementation and investigation plans
repos/             -- cloned source repos for analysis (gitignored except SOURCES.md)
  SOURCES.md       -- provenance for source repos (URLs, commits, descriptions)
  .gitignore       -- ignores all repo content, tracks only SOURCES.md
tasks/             -- project tracking (goals, workboard, decisions, lessons)
```

## Git Workflow

This repo lives at [REPO_URL]. Main is protected.

### Branch and PR Pattern

All changes go through pull requests:

1. **Branch** from main with a descriptive name (e.g., `add-failure-scenarios`, `update-cost-baseline`)
2. **Commit** with clear messages explaining what and why
3. **Push** and open a PR: `git push -u origin <branch>` then `gh pr create --title "..." --body "..."`
4. **User merges** via GitHub UI (Claude cannot merge — main is protected)
5. **Pull** after merge: `git pull origin main && git fetch --prune`

### Post-PR Discipline

Once a PR has been raised on a branch, **do not push additional commits to that branch**. This avoids conflicts, stale review data, and dirty merge histories. If asked to add changes to a branch with an open PR, first check whether the PR has already been merged. If it has, work from a new branch off main.

### Working Directory Safety

Before any git operation (commit, push, branch), verify you are in the **project root** — not inside a cloned repo under `repos/`. Run `git rev-parse --show-toplevel` and confirm it matches this project's root. This prevents accidentally committing to an analysis repo instead of the project.

### Git Conventions

- Claude handles all git operations (branch, commit, push, PR creation)
- Commit messages include `Co-Authored-By: <Model & Version> <noreply@anthropic.com>` (use the actual model powering the session)
- PR descriptions summarise content and context
- Delete source branch on merge
- Branches should be short-lived and focused — no long-running isolated branches with heavy divergence from main

## Workflow Orchestration

### 1. Project Isolation

- Each project is independent. **Do not load memories, context, or conventions from other projects** unless the user explicitly tells you to.
- Domain drift is a critical risk — assumptions from one project can silently corrupt another.
- If you need cross-project information, ask the user first.

### 2. Project Bootstrap Check

- Before starting work, check whether the project's required files are still placeholders (e.g., `[Project Name]`, `[REPO_URL]`, `[Product name and description]`).
- If key information is missing, **inform the user and ask if they want to populate it now** before proceeding with other work.
- Don't silently work around missing project context.

### 3. Plan Mode Default

- Enter plan mode for ANY non-trivial task (3+ steps or architectural decisions)
- If something goes sideways, STOP and re-plan immediately — don't keep pushing
- Use plan mode for verification steps, not just building
- Write detailed specs upfront to reduce ambiguity
- **Plans are project documents** — write them to `docs/plans/`, not ephemeral locations. Keep this directory pruned: remove plans that are fully executed or superseded.

### 4. Tiger Team Dispatch

This project has a **Lifecycle Engineering Tiger Team** — six senior-level agent profiles in `agents/` that provide multi-discipline analysis. The orchestrator (you) composes and launches them. Full team norms, coverage patterns, and escalation rules are in `agents/team-charter.md` — read it at dispatch time, not here.

| Shorthand | Profile | Model |
|-----------|---------|-------|
| SRE | agents/sre.md | opus |
| DEV | agents/dev.md | opus |
| DBE | agents/dbe.md | opus |
| QA | agents/qa.md | sonnet (escalate to opus for deep work) |
| SEC | agents/sec.md | opus |
| GA | agents/ga.md | sonnet (escalate to opus for deep work) |

**Dispatch protocol:** Read `agents/team-charter.md` + `agents/standards.md` + `agents/<role>.md` → read onboarding docs listed in the profile → if task matches a skill in the profile's `## Skills` section, read that skill file → compose prompt with charter norms, standards, role identity, project context, and task → launch via `Agent` tool → report findings attributed to the role.

Multiple roles can run in parallel. The user can invoke by shorthand, description, or ask for a round-table/adversarial review — see `agents/team-charter.md` for coverage patterns.

### 5. Agent Enrichment

- As the project progresses and you learn about technologies, pain points, or constraints relevant to an agent role, **update that agent's `Project-Specific Context` section** in their profile. Commit these updates alongside related work.
- Keep entries factual and terse — this is reference data, not narrative.
- When you notice a repeatable procedure emerging (same type of analysis done more than once), **recommend creating a skill** for it. Don't auto-create — flag it to the user with the pattern you've observed and which role(s) would use it.

### 6. General Subagent Strategy

- Use subagents liberally to keep main context window clean
- Offload research, exploration, and parallel analysis to subagents
- For complex problems, throw more compute at it via subagents
- One task per subagent for focused execution

### 7. Self-Improvement Loop

- After ANY correction from the user: update `tasks/lessons.md` with the pattern
- Write rules for **yourself** that prevent the same mistake
- Ruthlessly iterate on these lessons until mistake rate drops
- Review lessons at session start
- Use the memory system (`~/.claude/projects/`) for cross-session patterns that apply globally

### 8. Verification Before Done

- Never mark a task complete without proving it works
- Diff behavior between main and your changes when relevant
- Ask **yourself**: "Would a staff engineer approve this?"
- Run tests, check logs, demonstrate correctness

### 9. Demand Elegance (Balanced)

- For non-trivial changes: pause and ask "is there a more elegant way?"
- If a fix feels hacky: "Knowing everything I know now, implement the elegant solution"
- Skip this for simple, obvious fixes — don't over-engineer
- Challenge your own work before presenting it

### 10. Autonomous Bug Fixing

- When given a bug report: just fix it. Don't ask for hand-holding
- Point at logs, errors, failing tests — then resolve them

### 11. Source Repositories

- Repos cloned for analysis go in the `repos/` directory, not scattered elsewhere.
- Every cloned repo must be recorded in `repos/SOURCES.md` with its URL, branch/commit, and purpose.
- The `repos/.gitignore` excludes all repo content from version control — only `SOURCES.md` and `.gitignore` are tracked.
- When cloning a new repo, update `SOURCES.md` immediately.

### 12. Diagrams

- Diagrams use **Mermaid** syntax and are saved as `.md` files in the `diagrams/` directory (not `.mmd`).
- **Validate Mermaid syntax on creation** — check for common errors (unclosed brackets, invalid node IDs, missing arrows) before committing.
- Name diagram files descriptively (e.g., `data-flow-ingestion.md`, `auth-sequence.md`).

## Task Management

All project artifacts live in `tasks/` relative to this file.

| File | Purpose | Update Frequency |
|------|---------|-----------------|
| goals.md | Project north star — what we're building, why, principles, non-goals | Rarely (direction changes only) |
| workboard.md | Active work — status, owner, next steps, closure notes | Every session |
| decisions.md | Decision log — what was decided, why, when | When decisions are made |
| lessons.md | Mistake patterns and rules to prevent recurrence | After corrections |

## Session Anchor (Compression-Resilient)

**Before starting ANY task:**

1. `git pull origin main` — sync with remote (others may have pushed)
2. `git status` — confirm you're on main with clean working tree
3. Read `tasks/goals.md` — re-establish project intent
4. Read `tasks/workboard.md` — understand current state
5. Read `tasks/decisions.md` — check recent decisions
6. Read `tasks/lessons.md` — review mistake patterns and rules to prevent recurrence
7. **Bootstrap check** — if project files still contain placeholders (`[Project Name]`, `[REPO_URL]`, etc.), inform the user and ask if they want to populate them before proceeding

This instruction lives in CLAUDE.md (system context) and **survives context compression**. File contents read during conversation will be compressed out of history — always re-read at task boundaries rather than assuming prior reads are still in context. If uncertain whether project files reflect current context, re-read them.

## Closure Discipline

Before context-switching away from active work:

- Update the workboard entry with current status and remaining work
- If work is complete, mark it done with a one-line closure note
- If work is abandoned or deferred, say why
- If a decision was made during the work, add it to `decisions.md`

## Workflow

1. **Read First**: Check `goals.md` and `workboard.md` before starting
2. **Claim Work**: Add/update your item in `workboard.md` before implementing
3. **Track Progress**: Update status as you go
4. **Close Cleanly**: Status + closure note before moving on
5. **Log Decisions**: Any non-obvious decision goes in `decisions.md`
6. **Capture Lessons**: Update `lessons.md` after corrections

Note: Built-in task tools (TodoWrite/TodoRead) are for ephemeral in-conversation tracking. The `tasks/` markdown files persist across sessions and provide the project's memory.

## Core Principles

- **Simplicity First**: Make every change as simple as possible. Impact minimal code.
- **No Laziness**: Find root causes. No temporary fixes. Senior developer standards.
- **Minimal Impact**: Changes should only touch what's necessary. Avoid introducing bugs.

## Analysis & Communication Standards

Full standards are in `agents/standards.md` — read at session start and include when dispatching agents. The key principles:

- **Reliability over delivery**: say "I don't know" rather than guess. Distinguish known data from estimates.
- **Answer directly**: questions are questions, not invitations to reframe or add strategy.
- **Real data only**: query before estimating. Never assume homogeneity.
- **User's goals are north star**: provide data to inform decisions, don't make the decisions.
- **Good enough beats perfect**: match precision to the decision being made.

## Project Context

**Product:** [Product name and description] **Stack:** [Languages, frameworks, databases] **Infrastructure:** [Cloud provider, compute model, regions]

## Reading Order (start here)

1. `docs/...` — [description]
2. `repos/SOURCES.md` — provenance for any cloned source repositories
3. `diagrams/` — architecture and data flow diagrams
