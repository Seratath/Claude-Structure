# Sources

This directory holds live clones of external structure/template repos referenced by the workspace orchestrator.

## What lives here

- `Claude-Structure/` — a clone of https://github.com/Seratath/Claude-Structure. Provides workspace templates, shared agent library, and shared skills. Claude reads from here when scaffolding new projects.

## How to update

```
cd Sources/Claude-Structure
git pull
```

## Rules

- **Don't edit files here to customise a project.** Edit the project's own copy. Sources/ is upstream.
- **Don't commit Sources/Claude-Structure/** from the workspace — it's already its own repo and is gitignored at the workspace level.
- **If you delete this folder,** the workspace orchestrator will notice on next session and ask before restoring it. Deletion is respected, not auto-healed.
