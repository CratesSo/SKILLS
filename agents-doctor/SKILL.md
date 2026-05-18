---
name: agents-doctor
description: "Maintain AGENTS.md and LESSONS.md via cleanup, compression, and optional splitting."
---
# agents-doctor
Maintain `AGENTS.md` and `LESSONS.md` through cleanup, compression, and optional splitting.

## Target Discovery
- If user explicitly asks for global AGENTS, use `/Users/admin/.codex/AGENTS.md` and skip repo `LESSONS.md`.
- Determine repo root with `git rev-parse --show-toplevel`. If not in a git repo, use current working directory as the target root and report that assumption.
- Find `AGENTS.md` in target root and look for repo `LESSONS.md`.
  - If `AGENTS.md` is absent, stop and report missing path.
  - If repo `LESSONS.md` is absent, report that lesson classification was skipped and continue with inventory and cleanup planning.
- For repo-local targets, also read `/Users/admin/.codex/AGENTS.md` as the global baseline when present. Use it only to find local guidance that is already covered globally.

## Default UX
- Default invocation is audit-first. Don't edit files unless user explicitly asks to apply changes.
- Run planning phases sequentially and report proposed changes before applying edits.
- If user asks to apply changes, apply only confirmed items from latest report.
- If an apply request is ambiguous, apply only clearly named phases or items; otherwise ask before editing.
- Keep edits narrow and local to `AGENTS.md`, `LESSONS.md`, and generated `AGENTS_<topic>.md` reference files.

## Phase 1: Inventory
Inventory `AGENTS.md` and `LESSONS.md` when present before cleanup, lesson classification, or split planning. Collect only the evidence needed for a consolidated plan:
1. Current line count of `AGENTS.md` and `LESSONS.md` for before/after comparison.
2. `AGENTS.md` headings and high-value always-loaded sections.
3. `LESSONS.md` lessons that overlap existing `AGENTS.md` guidance.
4. Obvious stale, duplicate, or contradictory guidance.
5. Repo-local guidance already covered by global `/Users/admin/.codex/AGENTS.md`, when auditing a repo-local target.
6. Large situational sections that may be split after consolidation.

## Phase 2: Cleanup Plan
After inventory, audit current `AGENTS.md` before lesson classification so lessons can be mapped to intended canonical guidance instead of temporary duplicate text.
1. Redundancy: exact duplicates, overlap, repeated concepts, or rules covered by stronger local guidance.
2. Brevity: wording that can be compressed without losing meaning.
3. Freshness: stale paths, obsolete tools, outdated workflow steps, or repo facts contradicted by current files.
4. Low value: generic, past-state, or edge-case guidance that no longer earns always-loaded space.
5. Global coverage: for repo-local targets, generic local guidance already covered by `/Users/admin/.codex/AGENTS.md`.

Classify findings:
- `merge`: combine overlapping content into one canonical place.
- `compress`: shorten useful content without changing meaning.
- `remove`: delete exact duplicates, clearly covered duplicates, or generic guidance already covered by the same target `AGENTS.md`, global `/Users/admin/.codex/AGENTS.md`, or stronger active instructions.
- `needs confirmation`: changing it could alter meaning, priority, or repo-specific intent.
- `keep`: preserve because it remains useful or deletion would require judgment.

(Report `merge`, `compress`, and `remove` findings as safe candidates. Don't apply anything during the default audit.)
When a safe removal is based on global coverage, label it `remove (covered globally)` in the cleanup report.

Preserve by default:
- repo-specific invariants and constraints
- local guidance that narrows, overrides, or operationalizes global guidance for this repo
- hard-won behavior rules
- tool, signing, install, sandbox, validation, and workflow workarounds
- file and path anchors that help future agents navigate the repo
- safety, permission, and destructive-command constraints

## Phase 3: Lessons
After cleanup planning, classify every lesson in repo `LESSONS.md` against current `AGENTS.md`, the global baseline when present, plus Phase 2 cleanup plan before editing:
- `covered`: already handled by current or planned canonical `AGENTS.md` guidance.
- `merge`: should strengthen or clarify an existing/planned canonical rule.
- `new`: repo-wide repeatable guidance likely to help future agents across multiple tasks and not covered elsewhere.
- `keep`: useful but incident-specific, subsystem-narrow, historical, or not broad enough for `AGENTS.md`.
- `delete candidate`: obsolete, duplicated, vague, or low-value. Report only unless the user confirms deletion.

Report lesson edits:
1. Propose `merge` lessons into the relevant canonical `AGENTS.md` rule instead of creating duplicate guidance.
2. Propose `new` lessons for the most relevant existing section, or for a `## LESSONS` section at the end only if no better section exists.
3. Report `covered` lessons as absorb candidates that can be removed from `LESSONS.md` only if the user confirms.
4. Propose tighter wording only when it clearly improves reuse.
5. Report the resulting `LESSONS.md` renumbering that would happen after confirmed moves, merges, absorptions, or deletions.

## Phase 4: Split Plan
After lesson classification, audit final intended `AGENTS.md` for large situational guidance that can move to adjacent reference files without changing meaning. In audit-only mode, use the current file plus proposed cleanup and lesson changes as context.
- Good split candidates: repo-type guidance, work-mode runbooks, tool-specific procedures, rare workflows, and long examples that are not needed for most tasks.
- Don't split core rules, safety constraints, target discovery rules, short guidance where the pointer costs as much context as the original, or content whose meaning depends on nearby priority/order.

Score each split candidate from `1` to `5` to prioritize the report:
- `context savings`: expected reduction in always-loaded context.
- `lookup clarity`: how obvious it is when to open the reference.
- `preservation risk`: risk that moving changes meaning, priority, or usage.

(Don't create reference files during default audit. Report split candidates and require explicit confirmation before applying them.)

For each confirmed split:
1. Create `AGENTS_<topic>.md` beside the target `AGENTS.md`, using a lowercase underscore slug from the original section title.
2. Move the section nearly verbatim into the reference file.
3. Replace the original section with a concise pointer that includes the absolute reference path and a specific trigger condition.
4. Ensure the moved guidance exists in one canonical location only.

(Report all non-confirmed candidates as `needs confirmation` or `skipped`.)

## Apply Confirmed Edits
- When user confirms edits, apply cleanup, lesson, and split changes together so overlapping guidance becomes one canonical rule. Apply only confirmed items from latest report.
- For confirmed lesson moves, merges, absorptions, or deletions, renumber remaining `LESSONS.md` lessons consecutively from `1.` and validate moved or absorbed guidance appears exactly once.
- For confirmed splits, perform split validation after final `AGENTS.md` content is known.
- For confirmed global-coverage cleanup, prune only repo-local text that is generic and already covered globally; keep local repo-specific narrowing, exceptions, paths, command names, and operational details.

## Apply Validation
After applying any confirmed edits:
1. Re-read every touched file.
2. Confirm no unconfirmed item was changed.
3. Confirm moved lesson or split guidance exists in one canonical place.
4. Confirm pruned repo-local guidance is still covered by `/Users/admin/.codex/AGENTS.md` or a stronger active instruction.
5. Confirm every generated pointer uses the correct absolute path and resolves to an existing file.
6. Confirm reported line and bullet counts match the final files.

## Final Report
Return a compact phase ledger with visible Markdown using template below:

```md
### A ← Inventory
  1. **Target**: `<AGENTS.md path>`
  2. **Inputs**: `<LESSONS.md path, skipped, or skipped (global AGENTS target)>`
  3. **Global Baseline**: `<global AGENTS path, absent, or skipped (global AGENTS target)>`

### B ← Cleanup
  1. **Proposed**: `<items or None>`
  2. **Applied**: `<items or None>`
  3. **Needs Confirmation**: `<items or None>`

### C ← Lessons
  1. **Proposed**: `<merge/new/covered items or None>`
  2. **Applied**: `<items or None>`
  3. **Kept**: `<items or None>`
  4. **Confirm To Delete**: `<items or None>`

### D ← Splits
  1. **Proposed**: `<items or None>`
  2. **Applied**: `<AGENTS_<topic>.md files or None>`
  3. **Skipped / Needs Confirmation**: `<items or None>`

### E ← Counts
  1. **AGENTS.md**: `<before>` lines -> `<after>` lines
  2. **LESSONS.md**: `<before>` lines -> `<after>` lines
  3. **Generated References**: `<AGENTS_<topic>.md path: lines ... or None>`
```
(For audit-only runs, set all applicable `Applied` fields to `None (audit-only)`. If a phase made no changes, say so plainly. Include validation failures or skipped items in relevant section.)
