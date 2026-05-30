---
name: code
description: "Use only for complex coding tasks, refactoring, risky edits, dead code cleanup. Don't use for planning, simple tasks, style changes, or non-code tasks."
---
You must follow all rules below when implementing or editing code:

# CORE RULES
- Only touch files required for the task, plus adjacent cleanup needed for clean cut.
- Only add minimum code that fulfills requirement with nothing speculative.
- Always identify canonical path first, then hard cut to it.
- Never add features beyond what was asked.
- Never refactor things that are not broken.

## CODE RULES
- Never add helpers, wrappers, hooks, classes, types, interfaces, enums, config knobs, or option bags unless they remove more complexity than they add.
- Never widen types, function signatures, or data models with extra flags, optional fields, or parameters just to make changes fit.
- Never add fallback branches, parallel paths, compatibility shims, speculative extensibility, or generic wrappers without a real contract.
- Never add defensive code or overly defensive tests for impossible or unlikely scenarios.
- Always prefer boring code: obvious control flow, early returns, and explicit locals when readability improves.
- Always keep one-use logic inline unless hard to read; extract small helper near call site only when logic repeats 2+ times or clearly removes complexity.
- Always avoid tiny renaming helpers, callback pyramids, nested ternaries, split state choreography, and vague generic abstractions.
- Always prefer simple state shape and direct flow over sentinel values, boolean flag piles, optional-field bags, obsolete state, or indirection; reshape bad state instead of adding guards.
- Always isolate side effects in small orchestrators over hiding them in semantic helpers.
- Always delete dead code, stale helpers, redundant live paths, duplicate implementations, dead variants, unused assets, compatibility leftovers, and imports or variables orphaned by changes.
