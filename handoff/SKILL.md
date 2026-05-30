---
name: handoff
description: "Handoff current thread context to agent in newly created thread."
---
# $HANDOFF
Default invocation with no arguments uses Codex thread tools, not `HANDOFF.md`.

1. Infer current goals, done states, settled decisions, task-specific constraints, key workspace anchors, and blockers from active thread context to use in continuation packet.
2. Generate continuation packet for agent in new thread using the `## HANDOFF TEMPLATE` below; Always omit any reference or mention of codex Skills: `$skill` tags, `SKILL.md`, etc.
3. Create a new Codex background thread with `create_thread` in same project/workspace, using local environment:
   - `target.type`: `project`
   - `target.projectId`: current saved project/workspace id
   - `target.environment.type`: `local`
   - `prompt`: the continuation packet plus an instruction to continue from that context
4. If `create_thread` returns a thread id, treat creation as verified.
5. After creation verified, rename new thread to `Handoff: <two word description>` with `set_thread_title`.
6. If all steps completed, output a level-1 Markdown header link to the new thread, using exact format `# [Handoff Thread](codex://threads/<thread id>)`.

## $HANDOFF A
If user invokes this skill with `A` after it, proceed with default invocation steps, but after creation verified, archive original/current thread with `set_thread_archived`.

## $HANDOFF SAVE
- If user invokes this skill with `save` after it, generate a continuation packet using `## HANDOFF TEMPLATE` below and save as `HANDOFF.md` in current repo root.
- If `HANDOFF.md` already exists, overwrite it.
- Say `Done` after writing `HANDOFF.md`.

## $HANDOFF LOAD
- If user invokes skill with `load` after it, fully read `HANDOFF.md` from current repo root, treating it as continuation context, then await further instruction.
- If `HANDOFF.md` is missing, say `HANDOFF.md missing`.
- If `HANDOFF.md` was present and read, say `Ready`.

## UNKNOWN ARGUMENTS
If user invokes skill with any argument other than `save` or `load`, show brief usage:
- `$handoff save`: write `HANDOFF.md`
- `$handoff load`: read `HANDOFF.md`

## HANDOFF TEMPLATE
Use template below when creating handoff thread or making `HANDOFF.md`:

CONTEXT:
This is context from a previous thread; Await further instructions before continuing.

PREVIOUS THREAD SUMMARY:
`detailed summary of recent material and important work done in thread`

CURRENT TASK(S):
`describe current material objective(s)/task(s)`

SETTLED DECISIONS:
- `describe locked choice(s) or constraint(s)`

KEY ANCHORS:
- `list files, symbols, commands, or key factual anchors`

CURRENT BLOCKERS:
- `list material blockers or omit section if none`
