# Legacy Template

The original numbered-docs project template, preserved for reference.

## Why it's here

Earlier projects (Block Breaker, Hosting Game) were built with this structure before the current `base-project/` and `lifecycle-engineering/` templates existed. Keeping this here lets you:

- Review what was in the old format when migrating an existing project
- Understand why earlier projects have files like `02-GOAL-AND-PRINCIPLES.md`
- Pull structure or language from the old docs into a new-format project if useful

## Don't use this for new projects

For new work, use `base-project/` (default) or `lifecycle-engineering/` (SaaS/platform-specific team). The legacy format has been superseded because:

- It doesn't separate session anchors (CLAUDE.md) from content (tasks/, agents/)
- It doesn't support agent dispatch or a shared agent library
- It mixes goals, workboard, and changelog in a way that gets unwieldy as projects grow
- It has no built-in mechanism for milestone gating or decision tracking

## Migration notes

When migrating a legacy project to the new format, the overlay approach works well:

1. Leave the numbered docs in place (they're historical record)
2. Create `CLAUDE.md` at the project root (from `base-project/`)
3. Create `tasks/goals.md` by extracting the stable content from `02-GOAL-AND-PRINCIPLES.md`
4. Create `tasks/workboard.md` by extracting active items from `04-WORKBOARD.md`
5. Create `tasks/decisions.md` and `tasks/lessons.md` fresh (populate as things land)
6. Create `agents/` and copy relevant profiles from `Agents/`

Block Breaker's migration is the reference example.

## Files

- `00-README.md` — orientation
- `01-COLLABORATION-AND-ENGAGEMENT.md` — how humans and AI work together on the project
- `02-GOAL-AND-PRINCIPLES.md` — North Star (closest analogue to `tasks/goals.md`)
- `03-DESIGN-AND-REQUIREMENT.md` — design principles and requirements
- `04-WORKBOARD.md` — active work tracking (closest analogue to `tasks/workboard.md`)
- `05-CHANGELOG.md` — change history
