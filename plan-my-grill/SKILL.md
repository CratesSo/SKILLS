---
name: plan-my-grill
description: "Interrogate plans and designs with structured questions until they are handoff-ready and no blockers remain."
---
## OPENING
Lock intent through opening sequence before moving into adaptive questioning:

### PROMPT 1
`Prompt 1` must batch depth selection with first three intent questions:
- Ask user `How deep should planning go?`:
  - `Quick`: core blockers
  - `Standard`: balanced depth
  - `Thorough`: deeper plan
- After depth, ask first intent questions in same prompt: `goal`, `audience` (skip if already obvious or inferred), `success criteria`.

### PROMPT 2
Continue with the following three intent questions in `Prompt 2`:
- `scope boundaries`
- `non-goals` (explicit exclusions that prevent nearby work from being pulled into plan)
- `hard constraints`

## DEPTH SELECTION
Prompt count tracks prompts, not raw question count; A batched prompt counts as `1` prompt.
- `Quick` => `7` prompts (after intent locked, focus mainly on reducing user request ambiguity)
- `Standard` => `12` prompts (unless plan becomes robust enough for handoff with no edge-cases or blockers remaining)
- `Thorough` => `17` prompts (unless plan becomes robust enough for handoff with no edge-cases or blockers remaining)

### DOMAIN PACKS
After intent locked, use domain-specific question packs if relevant to user request; Don't walk every pack or use the examples as a strict checklist:
- `frontend`: user workflow, information architecture, state, accessibility, responsive behavior, empty/loading/error states.
- `backend`: API contracts, data model, persistence, permissions, failure modes, observability.
- `refactor`: behavior preservation, boundaries, migration path, test coverage, obsolete paths to remove.
- `migration`: source and target states, compatibility, rollout, rollback, data integrity.
- `debugging`: reproduction, expected behavior, observed behavior, likely fault boundary, verification.
- `feature addition`: expected behavior, UX, etc.
- `release`: rollout, monitoring, user communication, rollback, acceptance checks.

## QUESTION RULES
- Ask next question based on what removes highest impact blocker or ambiguity.
- If question can be answered by exploring code or environment, explore over asking.
- Never ask low risk detail questions unless detail is likely to distort plan or implementation.
- Never repeat or lightly rephrase answered questions.
- Revisit resolved points only if new info creates inconsistency or invalidates earlier answer.
- Maintain concise decision ledger after each answer:
  - `**Locked**`: explicit user decisions.
  - `**Assumed**`: low risk assumptions being carried forward.
  - `**Open**`: unresolved high impact blockers.
  - Keep ledger short and only show when it helps orient next question or final plan.
- If user gives conflicting answers, stop and resolve contradiction before asking around it or continuing plan.
- Call out weak, inconsistent, or underspecified choices directly.
  - Force real tradeoff decision if weak assumption would materially change implementation.
  - Never press low impact disagreements if risk is understood and choice locked.
- Always add a fire 🔥 emoji instead of "(recommended)" directly after the user selectable option you most recommend for each question.

### EDGE CASES
Ask edge-case questions when handling them can materially change plan, implementation, UX, data integrity, rollout, or test strategy:
- Edge case prompts don't count toward selected depth target.
- Stop edge case questions once edge cases are irrelevant or can be handled by obvious defaults.
- Discover candidate edge cases through exploration, reasoning, and user selected answers before prompting.
  - Examples: If potential code change might introduce new failure mode, explore code and use reasoning to identify what failure mode might be before asking how to handle it. If user selects answer that would introduce known edge case, ask how to handle that edge case before proceeding.

## QUESTION STYLE
Use `request_user_input` for questions that materially change plan, confirm important assumptions, or choose between real tradeoffs:
- Default to one high impact question at a time.
- Ask `2-3` questions in one prompt if they're tightly coupled and batching can close branches faster than asking one at a time.
- Never batch questions in same prompt when one answer could shape the next question or when option combinations could conflict.
- Hard Exception: opening prompts must follow `## OPENING` rules.
- Offer `3-4` meaningful mutually exclusive options.

## CONTINUATION
Ask "Keep going?" with three options at the selected depth target:
- `Continue`: continue asking as before
- `Stop here`: produce final plan
- `Three more`: ask three more, then ask "Keep going?" again after those three.

## DONE
When questions done or user indicates completion, output `<proposed_plan>` complete on intent, locked decisions, non-goals, hard constraints, assumptions, implementation, and tests.
- <proposed_plan> should not be concise/compact by default or be limited to a specific number of sections.
- <propose_plan> should include any additional sections that are relevant or needed to make plan more fleshed out and less ambiguous.
