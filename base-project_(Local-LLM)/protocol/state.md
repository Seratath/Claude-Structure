# Project State

> Live state file. PM reads this at the start of every turn. Logger Agent writes to this after every approved action. If this file is blank or missing, treat the project as a fresh session and run the session anchor checklist in protocol/core.md.

---

## Project Identity

**Name:** [project name]
**Goal summary:** [one sentence — what we are building and why]
**Current phase:** [bootstrap | prompt-improvement | planning | step-breakdown | execution | complete]

---

## Pipeline Position

**Last completed stage:** [none | prompt-approved | plan-approved | steps-approved | step-N-complete]
**Last approved output:** [file path or "none"]
**Next action:** [what the PM should do next]

---

## Active Jobs

| Job ID | Agent | Status | Started |
|---|---|---|---|

*Empty when no agents are running.*

---

## Rejection Counts (current session)

Tracks consecutive rejections per agent. Retrospective is eligible at 2+.

| Agent | Rejection count | Last rejection reason |
|---|---|---|

---

## Open Items

Things that need user input, unresolved decisions, or deferred work.

| Item | Type | Priority |
|---|---|---|

---

## Cycle Counter

Tracks completed pipeline cycles this session. Rebase is recommended after 2.

**Cycles completed this session:** 0
**Rebase due:** no

---

## Last Rebase

**Timestamp:** [ISO-8601 or "never"]
**Summary:** [one sentence — state of project at last rebase]

---

## Session Log (current session)

Brief log of approved actions this session. Logger Agent appends here.

| Timestamp | Action | Output |
|---|---|---|
