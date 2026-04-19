# Agent Library Index

Agents are role profiles that sub-agents adopt when dispatched. Pick the ones relevant to your project, copy them into your project's `agents/` folder, and enrich the Project-Specific Context section as the project grows.

Projects own their local copies. The library is the clean starting point.

## How to Use

1. Identify which roles your project needs (start small — add as work demands it)
2. Copy the relevant profile(s) into `agents/` in your project
3. Add the role to the dispatch table in your project's `CLAUDE.md`
4. Fill in Project-Specific Context as you learn about the project

## Generic (Project-Agnostic)

| Agent | File | Model | Purpose |
|-------|------|-------|---------|
| Growth & Alignment Analyst | `generic/ga.md` | sonnet / opus | Owns the North Star. Invoked at milestones and direction changes — not per task. Surfaces gaps, drift, and challenges to goals. |

## SaaS / Platform Engineering

| Agent | File | Model | Purpose |
|-------|------|-------|---------|
| Platform & Reliability Engineer | `saas/sre.md` | opus | Operability, deployment safety, observability, incident readiness |
| Application Services Engineer | `saas/dev.md` | opus | Application architecture, API design, service boundaries, developer experience |
| Database Engineer | `saas/dbe.md` | opus | Data integrity, schema design, migration safety, query performance |
| Quality & Validation Engineer | `saas/qa.md` | sonnet / opus | Test strategy, validation evidence, regression safety, acceptance criteria |
| Security & Compliance Engineer | `saas/sec.md` | opus | Threat modelling, attack surface, secrets, compliance frameworks |

## Game Development

| Agent | File | Model | Purpose |
|-------|------|-------|---------|
| *(coming soon)* | `game/` | — | Play engineer, systems modeller, UX/engagement, test/QA |

## Adding New Agents

When a repeatable role emerges that's materially different from existing ones:

1. Copy `agents/skills/_TEMPLATE.md` as a starting point for the profile structure
2. Name the file clearly: `<domain>/<role-shorthand>.md`
3. Add it to this index with a one-line description
4. If it's useful across projects, add it here; if it's project-specific, keep it in the project
