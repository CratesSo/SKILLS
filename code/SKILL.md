---
name: code
description: "Only use before complex or risky coding/planning/design work. Don't use for simple, straightforward, or obvious tasks."
---
# CORE RULES

Follow rules 1-9 when coding, planning, or designing:

## IMPLEMENTATION RULES

1. For every decision, ask what the best expert in that field would do and why they would reject your current choice; if you can name that reason, don't make the choice. Optimize for what that expert would judge correct, never for what satisfies the stated constraints most cheaply. Every trade-off you take must be stated to the user, never absorbed.

2. Before forming code, plans, or designs, and after each material implementation step, answer these questions and act according to their answer:
 - Is there any part of the code/plan/design that doesn't need to exist? If so, edit the code/plan/design to remove it.
 - Can the code/plan/design be simpler, more direct, or more elegant? If so, edit the code/plan/design to simplify it.
 - Can a standard library or already-canonical dependency be used? If so, use it.

## CODE RULES

3. Identify the canonical path, hard cut to it; Never introduce duplicate or parallel paths.
4. Prefer direct control flow, explicit locals, and simple state. Add abstractions, helpers, types, configuration, or model fields only when they remove more complexity than they add.
5. Never add any speculative features, extensibility, compatibility shims, generic wrappers, fallback branches, or widened interfaces without a real contract.
6. After implementing, search for and remove any obsolete or duplicate paths introduced by your changes before ending your turn.

## VALIDATION RULES

7. NEVER add defensive handling or tests for unlikely/unreachable states or states outside of production.
8. NEVER create or expand tests unless a focused test is simplest credible way to establish behavior not already proven at its owning boundary.
9. ALWAYS avoid any and all process/safety/correctness theater; Unless absolutely required or explicitly requested, don't create ledgers, hashes, proof bundles, completion dossiers, repeated review loops, or other artifacts whose sole purpose is to demonstrate diligence/safety/correctness.
