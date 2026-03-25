---
name: plan-my-grill
description: Interrogate plan or design until handoff-ready. Start with intent, explore facts first, challenge weak choices directly, prefer Plan mode clickable questions via `request_user_input`.
---

# Interrogate a plan / design until handoff-ready and no high-impact blockers remain.

## Start with intent:
- Goal
- Success criteria
- Audience
- Scope boundaries
- Constraints

## After intent is stable:
- Use hidden completeness frame, tracking what still matters, such as interfaces, data flow, failure modes, tests, and rollout.
- Ask the next question that removes highest-impact blocker.
- Route questions by blocker severity over following a rigid checklist.

## Question selection rules:
- If question can be answered by exploring codebase or environment, explore over asking.
- Don't ask low-risk detail questions unless missing detail is likely to distort plan or implementation.
- If something is underspecified, ask unless assumption is low-risk and unlikely to change implementation materially.
- Track resolved decisions and don't repeat or lightly rephrase answered questions.
- Revisit resolved points only if new information creates real inconsistency or invalidates earlier answer.
- Call out weak, inconsistent, or underspecified choices directly.
- Force a real tradeoff decision if a weak assumption would materially change implementation.
- Do not keep pressing on low-impact disagreements once risk is understood and choice is locked.

## If Plan mode active:
- Ask 18 questions minimum.
- Use `request_user_input` for questions that materially change the plan, confirm important assumptions, or choose between real tradeoffs.
- Prefer Codex app's clickable question UI over inline `a`/`b`/`c` answer menus.
- Default to 1 high-impact question at a time.
- You may ask 2-3 questions in 1 prompt if are tightly coupled and batching can close a branch faster with less back-and-forth.
- Offer only 4 meaningful mutually exclusive options and add 🔥 emoji instead of "(recommended)" for your most preferred option.

## If Plan mode inactive or `request_user_input` unavailable:
- Fall back to plain-text questions in chat.
- For each question provide 3-5 concise example answers labeled with letters: `a`,`b`,`c`, etc.
- Mark recommended answer with a 🔥 emoji.
- Keep options short enough that user can reply compactly like `1a, 2c, 3b`.
- If no example answers fit leave room for freeform answer.

## After 18 questions
- Ask "Should we keep going?" with three options: "Keep going", "Stop here", "Three more questions".
  - "Keep going" = continue asking questions as before.
  - "Stop here" = end questioning + produce final plan using info gathered.
  - "Three more questions" = ask three more before asking again.

## When to stop:
- When no high-impact unresolved blockers remain.
- If user says to stop.

## Final Output
- If questioning is done, produce full handoff-ready `<proposed_plan>` complete on intent / implementation, include tests / assumptions, avoid leaving decisions to implementer.
