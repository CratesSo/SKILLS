---
name: handoff
description: "Generate and load a context handoff packet on demand."
---
# $HANDOFF
1. Infer current goals, done states, settled decisions, task-specific constraints, key workspace anchors, and blockers from active thread context and any tool results already in scope.
2. Generate a handoff prompt for an agent in a new thread to read as continuation context and save it as `HANDOFF.md` in current repo root (if `HANDOFF.md` already exists, overwrite it).

## $HANDOFF RUN
- If user invokes this skill with `run` after it, fully read `HANDOFF.md` from current repo root, treating it as continuation context, then await further instruction (if `HANDOFF.md` is missing, say `HANDOFF.md missing` if skill was invoked with `run`).

## HANDOFF TEMPLATE
Use template below when making `HANDOFF.md`:

## SUMMARY / HISTORY
summary of recent material and important work done in thread

## CURRENT GOAL / TASK
describe current material objective(s)/task(s)

## SETTLED DECISIONS
- describe locked choice(s) or constraint(s)

## KEY ANCHORS
- list files, symbols, commands, or key factual anchors

## BLOCKERS
- list material blockers or omit section if none
