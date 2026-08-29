---
name: adr
description: "Use adr only for major, durable architectural decisions with costly reversal. Skip adr for routine, isolated, low-impact, or easily reversible implementation, configuration, tooling, or workflow changes."
---

# WORKFLOW
Work from the repo root and preserve unrelated worktree changes.
1. Read `docs/adr/index.md` and relevant ADRs; update an existing decision when no new durable decision exists.
2. Run `adr init docs/adr` only when the directory is missing.
3. Never hand-create or number ADR files. Create one with:
   - New decision: `adr new "<title>"`
   - Supersedes: `adr new -s <old> "<title>"`
   - Related: `adr new -l "<target>:Relates to:Related by" "<title>"`
4. Edit the generated ADR content into the lean format below.
5. Regenerate the index with `adr generate toc > docs/adr/index.md`; this intentionally replaces the index.
6. Validate with `adr list`, inspect the new links, and run `git diff --check`.

## ADR FORMAT
Use **Proposed** while undecided, **Accepted** after approval, and **Superseded** only through a replacement ADR. Keep short, concrete rationale in this exact shape:

# <title>
- Status: ...
- Context: ...
- Decision: ...
- Consequences: ...
