---
name: plan-my-grill
description: Interrogate plan or design until handoff-ready. Generic, domain-agnostic grill. Start with intent, explore facts first, challenge weak choices directly, prefer Plan mode clickable questions via `request_user_input`.
---

Interrogate a plan or design until handoff ready and no high impact blockers remain.

# BEFORE STARTING
- First prompt must batch 2 tightly coupled questions using `request_user_input`:
  - Ask user "How many prompts do you want?":
    - "15-20"
    - "10-15"
    - "5-10"
  - Ask first real intent question in that same prompt:
    - Goal + Audience
- Second prompt must happen immediately after opener using `request_user_input`:
  - Success Criteria
  - Scope Boundaries
  - Constraints
- Default targets:
  - `5-10` => `7-8`
  - `10-15` => `12-13`
  - `15-20` => `17-18`
- Example: User sets `5-10`, plan for `7-8` prompts unless plan becomes complete sooner or needs more by prompt `8`.
- Prompt count tracks prompts, not raw question count. A batched prompt counts as 1 prompt.
- After opener is answered, ask the second batched prompt immediately. Never pause just because prompt-count choice was answered.

# START WITH INTENT
- Goal + Audience
- Success criteria
- Scope boundaries
- Constraints

# AFTER INTENT IS STABLE
- Use hidden completeness frame, track what still matters like interface, data flow, failure modes, UX, rollout, etc.
- Ask next question that removes highest impact blocker.
- Route questions by blocker severity over following rigid checklist.

# QUESTION SELECTION RULES
- Reaching initial target never auto-stops. Continue to selected range top if high impact blocker remains.
- If question can be answered by exploring code or environment, explore over asking.
- Never ask low-risk detail questions unless detail is likely to distort plan or implementation.
- If something is underspecified, ask unless assumption is low-risk or unlikely to change implementation materially.
- Track resolved decisions and never repeat or lightly rephrase answered questions.
  - Revisit resolved points only if new info creates inconsistency or invalidates earlier answer.
- Call out weak, inconsistent, or underspecified choices directly.
  - Force real tradeoff decision if weak assumption would materially change implementation.
  - Never press low-impact disagreements if risk is understood and choice locked.
- Add 🔥 emoji instead of "(recommended)" for the most recommended option.

# PLAN MODE
- Use `request_user_input` for questions that materially change plan, confirm important assumptions, or choose between real tradeoffs.
  - Default to 1 high-impact question at a time.
  - Ask 2-3 questions in one prompt if they are tightly coupled and batching can close a branch faster than asking one at a time needlessly.
  - Hard exception: the first 2 prompts are always mandatory batched prompts.
  - First prompt = prompt-count selector + Goal + Audience.
  - Second prompt = Success criteria + Scope boundaries + Constraints.
  - Offer 3-4 meaningful mutually exclusive options.

# CONTINUATION
- Ask "Should we keep going?" with 3 options at selected range's top:
  - Count the 2 mandatory opening batched prompts toward that selected prompt range.
  - `Keep going`: continue asking as before
  - `Stop here`: produce complete final plan
  - `Three more`: ask 3 more, then ask again

# STOP
- If no high-impact unresolved blockers remain.
- If user says to stop.

# FINAL OUTPUT
- When questioning done, produce full handoff-ready `<proposed_plan>` complete on intent, implementation, tests, assumptions, avoid leaving decisions to implementer.
