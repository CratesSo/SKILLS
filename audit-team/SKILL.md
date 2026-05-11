---
name: audit-team
description: "Coordinate agentic audit workflows from scope mapping through triage and fixes."
---

# CANONICAL FLOW

1. Lock audit lens, scope, and exclusions.
2. Spawn one `explorer_deep` to map repo areas relevant to the audit lens and identify hotspots.
3. `explorer_deep` returns mapping and you close it.
4. Create non-overlapping `reviewer_heavy` or `reviewer_mid` slices by path or subsystem.
5. Spawn reviewer wave.
6. Wait for all reviewers to finish, then close them.
7. Triage reviewer output, reject weak findings, merge duplicates, and group accepted findings into non-overlapping implementation slices.
8. For tiny trivial accepted fixes, you may implement locally.
9. For non-trivial accepted fixes, you choose `worker_mini` or `worker` per implementation slice and spawn the worker wave.
10. Wait for all workers to finish, then close them.
11. Run final validation and report final output.

## PARENT RESPONSIBILITIES

- Exclude generated, build, cache, and lockstep artifact paths.
- Split `reviewer_heavy`/`reviewer_mid` slicing by non-overlapping path/subsystem ownership and prefer a small number of meaningful slices over fragmentation.
- Split implementation by non-overlapping write scope or shared root cause.
- Use `worker_mini` for one local root cause, small file set, low reconciliation risk.
- Use `worker` for broader or riskier slices, cross-file invariants, or heavier reconciliation.
- Spawn workers directly only after the full reviewer wave has finished and triage accepted implementation work.

## PARENT -> EXPLORER_DEEP PROMPT

Use the shape INSIDE the next fenced block below when spawning `explorer_deep`.

```text
Don't investigate findings deeply or triage findings. Your purpose is only to map repo areas relevant to the audit lens and identify likely audit hotspots for other agents to run a deeper pass on. Never spawn subagents.

GOAL:
[actionable description/context of audit lens]

SCOPE:
[paths, subsystems, or repo areas included]

AVOID:
[generated, build, cache, lockstep artifact, or out-of-scope paths]

RETURN:
- Relevant repo areas and why they matter.
```

## PARENT -> REVIEWER PROMPT

Use the shape INSIDE the next fenced block below when spawning `reviewer_heavy` or `reviewer_mid`.

```text
Never spawn subagents.

GOAL:
[describe reviewer slice with actionable info/context]

SCOPE:
[relevant paths or files owned by slice each on a new line]

AVOID:
[areas to avoid that are out of scope or covered by other slices or parallel reviews]
```

## PARENT TRIAGE RULES

- Keep only accepted findings worth implementing.
- Group accepted findings into implementation slices by shared files or shared root cause.
- Keep write scopes non-overlapping when parallel workers are used.
- Compress each implementation slice into a small execution brief before spawning a `worker` or `worker_mini`.
- If zero accepted findings remain after triage, skip implementation and report no accepted findings.

## PARENT -> WORKER PROMPT

- If one or more non-trivial implementation slices are accepted after triage, and only after the full reviewer wave has finished, spawn the required `worker` or `worker_mini` agents.
- Use the shape INSIDE the next fenced block below when spawning `worker` or `worker_mini`:

```text
Never spawn subagents.

GOAL:
[describe task with enough detail for worker to implement]

FILES:
[exact files needed to implement, each on a new line]

AVOID:
[overlap delegated in other worker slices to avoid]
```

## FINAL OUTPUT

Return the following response body using shape INSIDE the fenced block below after validation:

```md
## ACCEPTED FINDINGS
- **title**: [concise description]

## FIXES IMPLEMENTED
- **title**: [concise description]

## VALIDATION
- [concise bullets of tests done]

## RESIDUAL ISSUES
- [concise bullets]
```
