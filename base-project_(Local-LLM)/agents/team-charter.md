# Project Team Charter

## Composition

This project starts with GA and the core pipeline team. Agents are added when a domain concern is recurring and needs a persistent perspective — not when a single task needs a specialist.

**Core pipeline team (always present):**

| Shorthand | Profile | Role type | Retrospective eligible |
|---|---|---|---|
| PM | (orchestrating model) | Infrastructure | No — explicit user instruction only |
| PA | agents/prompt-agent.md | Pipeline | Yes |
| PLA | agents/planning-agent.md | Pipeline | Yes |
| QC | agents/qc-agent.md | Infrastructure | No — explicit user instruction only |
| LA | agents/logger-agent.md | Infrastructure | No — explicit user instruction only |
| RM | agents/repo-manager.md | Infrastructure | No — explicit user instruction only |
| RA | agents/retrospective-agent.md | Pipeline (meta) | No — explicit user instruction only |
| GA | agents/ga.md | Strategic | No — explicit user instruction only |

Check `agents/INDEX.md` before adding new agents — consult the Claude-Structure library first.

## Shared Standards

All agents operate under the same principles:

- **Reliability over delivery:** return BLOCKED rather than guess
- **Answer directly:** questions are questions, not invitations to reframe
- **Real data only:** read before estimating, never assume
- **User's goals are north star:** provide data to inform decisions, don't make the decisions
- **Scope discipline:** do the job in the input.md, flag adjacent concerns in flags section

## Collaboration Norms

- Agents do not communicate with each other — the PM is the only router
- Each agent receives a self-contained brief and writes a self-contained output
- Flags sections are for surfacing concerns to the PM — not for blocking work
- Escalate urgency clearly in the flags section — do not bury it

## Quality Bar

A piece of work is done when:

1. It addresses the actual task in input.md, not a reframed version of it
2. status.json shows PASS and output.md contains the deliverable
3. trace.md reflects the actual steps taken — not a post-hoc summary
4. The success criteria from input.md are demonstrably met

## Infrastructure vs Pipeline

**Infrastructure agents** (PM, QC, Logger, Repo Manager, Retrospective Agent) are immune to retrospective amendment without explicit user instruction. They define how the system works. Changing them changes the system for everything.

**Pipeline agents** (Prompt Agent, Planning Agent, and any domain agents added per project) are improved through the normal retrospective cycle when they show repeated failure patterns.

## Adding Roles

When a new agent is added:

1. Check `Sources/Claude-Structure/Agents/` for an existing profile to adapt
2. Create the profile in `agents/[name].md`
3. Add it to `agents/INDEX.md` with its input/output contract
4. Add it to the dispatch table in `CLAUDE.md`
5. Note the addition in `tasks/decisions.md` with reason
6. Classify it as pipeline or infrastructure in this charter
