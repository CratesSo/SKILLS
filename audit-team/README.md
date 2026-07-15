# audit-team <img src="./assets/icon.png" width="40" alt="audit-team icon">

**Runs a staged audit flow using scoped waves of subagents.**

**Locks the audit lens, then validates after the delegated run finishes.**

## Note

*This skill is optimized for specific, pre-configured subagents:*

- `explorer_deep`: Use escalated read-only mapping when standard exploration is insufficient, the code path spans multiple modules, or deeper local evidence is needed.
- Reviewer agents: Perform scoped, read-only review work.
- Worker agents: Implement accepted findings within assigned write scopes.

## How to use

1. Type `$audit-team <audit lens>`.
2. Follow the parent-led audit, mapping, triage, implementation, and validation flow.

### Examples

- `$audit-team repo wide, correctness`
- `$audit-team back-end, performance`
- `$audit-team frontend, security`

## Version

Current version: v1.6.0

## Install

`npx skills@latest add CratesSo/skills/audit-team`
