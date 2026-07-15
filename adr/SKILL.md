---
name: adr
description: "Use to create ADRs when any durable change affects architecture, tooling, data shape, workflow, repo conventions, or agent behavior. Skip for low-impact or temp changes."
---
Skip for minor or routine changes that don't have durable or material impact, temp experiments, simple bug fixes, or decisions already captured.

# Create Or Relate
Create in `MEMOS/adr/`; If not present, make folder -> init `adr init MEMOS/adr`.
- New durable decision: `adr new <title>`
- Replacement for earlier decision: `adr new -s <old> <title>`
- Related but not superseding: `adr new -l "<target>:Relates to:Related by" <title>`
- Create or update index after creating or updating ADR: `adr-log -d MEMOS/adr -i MEMOS/adr/index.md`

## ADR Format
Keep ADRs lean; Use short bullets and concrete rationale:
- `Title`
- `Status`
- `Context`
- `Decision`
- `Consequences`

## Report
Include ADR changes at end of response using shape below:

```md
## ADR <Created/Updated>
- <markdown link to ADR>
```
