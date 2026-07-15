---
name: handoff
description: "Create a new continuation thread from current context."
---

# Instructions
1. Infer current goals, completed work, settled decisions, task-specific constraints, key anchors, and blockers from current thread context.
2. Build a continuation packet using the template below and keep it focused on what the next thread needs to continue cleanly. Omit any reference or mention of Codex Skills, including `$skill` tags, `SKILL.md`, and skill names.
3. Use `create_thread` to create a new background thread in the current project and local environment with that packet:
   - `target.type`: `project`
   - `target.projectId`: current saved project/workspace id
   - `target.environment.type`: `local`
   - `prompt`: continuation packet plus instruction to continue from that context
4. After success, output only `::created-thread{threadId="<thread id>"}`.

## Handoff Template
Use this template for new thread:

```text
CONTEXT:
This is context from a previous thread. Await further instructions.

PREVIOUS THREAD SUMMARY:
<detailed summary of important work completed so far>

CURRENT TASK(S):
<current objective(s) to carry forward>

SETTLED DECISIONS:
- <locked decisions, constraints, or conventions>

KEY ANCHORS:
- <important files, symbols, commands, or facts>

CURRENT BLOCKERS:
- <material blockers (omit if none)>
```
