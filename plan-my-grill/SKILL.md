---
name: plan-my-grill
description: "Interrogate plans and designs with structured questions until they are handoff-ready."
---
# plan-my-grill

Interrogate a plan or design until handoff ready and no high impact blockers remain:

## BEFORE STARTING

First prompt must batch `2` tightly coupled questions:

- Ask user `How many prompts do you want?`:
  - `15-20`
  - `10-15`
  - `5-10`
- Ask first intent question in that same prompt: `goal`+`audience`

Second prompt must happen immediately after opener:

- `success criteria`
- `scope boundaries`
- `constraints`

Default Targets:

- `5-10` => `7-8`
- `10-15` => `12-13`
- `15-20` => `17-18`

Example: User picks `5-10`, plan for `7-8` prompts unless plan becomes complete sooner or needs more by prompt `8`.

- Prompt count tracks prompts, not raw question count. A batched prompt counts as `1` prompt.
- Count the two mandatory opening batched prompts toward that selected prompt range.

## START WITH INTENT

- `goal`+`audience`
- `success criteria`
- `scope boundaries`
- `constraints`

## AFTER INTENT LOCKED

Use a hidden completeness frame and track what still matters like interface, data flow, failure modes, UX, rollout, etc.

- Ask the next question based on what removes the highest impact blocker.
- Route questions by blocker severity over following rigid checklist.

## QUESTION RULES

- Reaching initial target never auto stops. Continue to selected range top if high impact blocker remains.
- If question can be answered by exploring code or environment, explore over asking.
- Never ask low risk detail questions unless detail is likely to distort plan or implementation.
- If something is underspecified, ask unless assumption is low risk or unlikely to change implementation materially.
- Track resolved decisions, never repeat or lightly rephrase answered questions.
- Revisit resolved points only if new info creates inconsistency or invalidates earlier answer.
- Call out weak, inconsistent, or underspecified choices directly.
  - Force real tradeoff decision if weak assumption would materially change implementation.
  - Never press low impact disagreements if risk is understood and choice locked.
- Always add a fire 🔥 emoji instead of "(recommended)" directly after the user selectable option you most recommend for each question.

### EDGE CASES

When a change plausibly introduces edge cases, spend at least `2` extra distinct prompts on edge-case decisions. If edge cases are complex, ask more until edge case handling is locked:

- Edge case prompts don't count toward selected prompt range.
- If changes won't plausibly introduce edge cases, skip edge case prompts.
- Discover candidate edge cases through exploration, reasoning, and user selected answers before prompting. Examples: If a potential code change might introduce a new failure mode, explore code and use reasoning to identify what that failure mode might be before asking how to handle it. If user selects an answer that would introduce a known edge case, ask how to handle that edge case before proceeding.

## QUESTION STYLE

Use `request_user_input` for questions that materially change plan, confirm important assumptions, or choose between real tradeoffs:

- Default to one high impact question at a time.
- Ask `2-3` questions in one prompt if they're tightly coupled and batching can close branches faster than asking one at a time.
- Hard Exception: The first `2` prompts are always mandatory batched prompts.
- First Prompt = `prompt-count selector`+`goal`+`audience`.
- Second Prompt = `success criteria`+`scope boundaries`+`constraints`.
- Offer `3-4` meaningful mutually exclusive options.

## CONTINUATION

Ask "Keep going?" with three options at user selected range top:

- `Keep going`: continue asking as before
- `Stop here`: produce final plan
- `Three more`: ask three more, then ask "Keep going?" after that

## STOP

Stop when no high impact unresolved blockers remain or user says to stop.

## DONE

When questioning done, produce full handoff-ready `<proposed_plan>` complete on intent, implementation, tests, assumptions, avoid leaving decisions to implementer.
