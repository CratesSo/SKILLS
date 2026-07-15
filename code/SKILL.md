---
name: code
description: "Only use immediately before complex or risky code implementation or cleanup."
---

Follow rules below when coding:

## CHECK RULES
Before, during, and after implementing, ask:
1. Does this code need to exist? If doesn't need to exist, simplify or remove it.
2. Can this code or solution be more elegant? If it can be more elegant or simpler, make it so.
3. Can a standard library do it? If yes, use it.
4. Is there already a usable installed dependency? If yes, use it.

## CODE RULES
- Always identify canonical path first, then hard cut to it.
- Always avoid adding duplicate/redundant code or parallel paths; If any found, clean it up.
- Never add any speculative features or features beyond those required or requested.
- Never add any helpers, wrappers, hooks, classes, types, interfaces, enums, config knobs, or option bags unless they remove more complexity than they add; If you did, clean them up.
- Never widen any types, function signatures, or data models with extra flags, optional fields, or parameters just to make changes fit; If you did, clean it up.
- Never add any fallback branches, parallel paths, compatibility shims, speculative extensibility, or generic wrappers without a real contract.
- Always prefer boring code like obvious control flow, early returns, explicit locals, etc.
- Always avoid adding any tiny renaming helpers, callback pyramids, nested ternaries, split state choreography, and vague generic abstractions.
- Always use simple state shape and direct flow instead of sentinel values, boolean flag piles, optional-field bags, obsolete state, or indirection; Reshape any bad state instead of adding guards.