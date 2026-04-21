---
name: slop-team-six
description: "Run an execution-first cleanup sweep that maps cleanup lanes, proves relevance, edits in waves, and validates narrowly. Use only when explicitly invoked for cleanup sweeps."
---

# slop-team-six

Run execution-first cleanup sweep. Scan repo, activate relevant cleanup lanes, prove relevance before edits, execute in two waves, review risky work, validate narrowly, and report by lane. Follow instructions below carefully and exactly:

## DEFAULTS

- Default scope is whole repo.
- Default stance is aggressive cleanup with evidence.
- Use repo-native tools when present. If a useful tool is absent, stop and ask permission before installing it.
- Always spawn agents with `fork_context: false`.

## REFERENCE LOADING

- Read spawned-agent prompt references only before spawning that agent.
- Read `references/tooling.md` during preflight and build a parent-owned tool inventory before Wave 1 starts.
- Pass lane reference paths to Wave 1 agents; do not load lane references in the parent unless needed to resolve ambiguity.
- Do not ask Wave 2 or reviewer agents to read lane references. Pass them parent-synthesized validated briefs instead.

## CANONICAL FLOW

1. Read `references/navigator.md`, then spawn `navigator` agent to map repo structure, exclusions, tool clues, and cleanup hotspots.
2. While `navigator` works, run `preflight` check and read `references/tooling.md`.
3. When `navigator` is done, map its cleanup hotspots to lanes and decide which lanes are active, skipped, or merged.
4. Resolve tool availability before Wave 1. If a useful missing tool is needed, stop and ask the user before installing it.
5. Read `references/wave1-cleanup.md`, then spawn read-only `cleanup` agents for `ACTIVE` or `MERGE` lane assignments with lane reference paths, approved commands, files, and avoid lists.
6. When all `cleanup` agents have finished, triage `Wave 1` results into validated implementation briefs.
7. When `Wave 1` results are triaged, read `references/wave2-worker.md`, then spawn `Wave 2` worker agents only for validated implementation using the parent-synthesized brief.
8. For higher-risk completed lanes, read `references/reviewer.md`, then spawn `reviewer` with changed files, validation state, and parent-synthesized lane constraints.
9. Run narrowest useful validation when fully complete.
10. Return track-by-track summary with risks and leftovers.

## PREFLIGHT

`preflight` means finding:

- languages in use
- workspace layout
- type systems and compiler configs
- available analysis tools by language, using `references/tooling.md` as the command matrix
- repo-native test, lint, or check commands
- obvious generated, vendor, cache, dist, build, coverage, and lockfile areas to exclude
- available tools and real runnable commands for each active lane

Read `references/tooling.md` during preflight. Wave 1 must not start until tool availability is known and each Wave 1 handoff lists usable commands.

## Navigator Brief

Read `references/navigator.md` immediately before spawning `navigator`.

## EIGHT LANES

These are the cleanup lanes. Keep in this order:

1. Dedupe and consolidation
2. Shared type consolidation
3. Unused code discovery and removal
4. Circular dependency removal
5. Weak type replacement
6. Unnecessary defensive error handling removal
7. Legacy, fallback, and deprecated path removal
8. AI slop, stubs, and low-value comments cleanup

Don't force all eight lanes to edit (execution is adaptive).

Each lane must end in one of three states before spawning `Wave 2`:

- `ACTIVE`: enough evidence to edit
- `SKIP`: repo does not meaningfully support lane
- `MERGE`: lane overlaps another lane enough that one worker should own both

## LANE ASSIGNMENT CONTRACT

Before spawning `Wave 1`, assign each agent exactly one `ACTIVE` lane or one explicit `MERGE` group.

Use `references/wave1-cleanup.md` as the source of truth for required Wave 1 handoff fields. If a lane is `MERGE`, list every lane in the group and every lane reference path the agent must read.

### Lane References

Pass specific lane references to `Wave 1` cleanup agents as discovery playbooks for lanes marked `ACTIVE` or `MERGE` without reading them yourself:

- Lane 1: `references/lanes/lane-1-dedupe.md`
- Lane 2: `references/lanes/lane-2-shared-types.md`
- Lane 3: `references/lanes/lane-3-unused-code.md`
- Lane 4: `references/lanes/lane-4-circular-deps.md`
- Lane 5: `references/lanes/lane-5-weak-types.md`
- Lane 6: `references/lanes/lane-6-defensive-errors.md`
- Lane 7: `references/lanes/lane-7-legacy-fallbacks.md`
- Lane 8: `references/lanes/lane-8-ai-slop.md`

## WAVE 1: EVIDENCE

For each `ACTIVE` or `MERGE` lane assignment, spawn a read-only `cleanup` agent to gather evidence-backed findings for parent triage.

Use `references/tooling.md` to build the approved command list for each Wave 1 handoff. If a needed tool is absent, stop and get permission before spawning Wave 1.

### Cleanup Brief

Read `references/wave1-cleanup.md` immediately before spawning `cleanup` agents for `Wave 1`. Fill every lane assignment field in the prompt.

## TRIAGE

You own triage. Never pass raw `Wave 1` output straight into edits.

Before `Wave 2`:

- Merge duplicate findings.
- Reject weak or overlapping findings.
- Collapse related lanes when they share the same files or root cause.
- Decide which lanes need `worker_mini` versus `worker`.
- Convert accepted Wave 1 findings into a validated implementation brief with exact files, edits, lane constraints, risks, and validation expectations.

## WAVE 2: EXECUTION

`Wave 2` implements only validated cleanup work:

- Use `worker_mini` for narrow, obvious cleanup slices.
- Use `worker` for cross-file or high risk cleanup slices.
- Keep write scopes non-overlapping when parallel workers run.

### Worker Brief

Read `references/wave2-worker.md` immediately before spawning worker agents for `Wave 2`. Fill the validated implementation brief fields in the prompt.

### Reviewer Brief

Read `references/reviewer.md` immediately before spawning `reviewer`. Fill the parent-synthesized lane constraints, changed files, and validation state.

## VALIDATION

Run narrowest useful validation for changed scope:

- Prefer lane-relevant checks first.
- Use repo-native tests, compilers, linters, and analyzers.

## FINAL RESPONSE

Keep final response concise and return results grouped by lane, even if multiple lanes merged during execution, using the template inside the fenced block below:

```md
## PREFLIGHT

- **Languages:** [list languages]
- **Tools Used:** [list tools]
- **Exclusions:** [list exclusions]

## LANE STATUS

- **Lane 1:** `ACTIVE` | `SKIP` | `MERGE`
- **Lane 2:** `ACTIVE` | `SKIP` | `MERGE`
- **Lane 3:** `ACTIVE` | `SKIP` | `MERGE`
- **Lane 4:** `ACTIVE` | `SKIP` | `MERGE`
- **Lane 5:** `ACTIVE` | `SKIP` | `MERGE`
- **Lane 6:** `ACTIVE` | `SKIP` | `MERGE`
- **Lane 7:** `ACTIVE` | `SKIP` | `MERGE`
- **Lane 8:** `ACTIVE` | `SKIP` | `MERGE`

## CHANGES BY LANE

### Lane n:

- **EVIDENCE:** [brief summary]
- **EDITS:** [brief summary]
- **VALIDATION:** [brief summary]
- **RISKS:** [brief summary]

## RESIDUAL

- [blockers, deferred lanes, or remaining risks]
```
