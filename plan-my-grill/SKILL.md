---
name: plan-my-grill
description: Interrogate plan or design until handoff-ready. Start with intent, explore facts first, challenge weak choices directly, prefer Plan mode clickable questions via `request_user_input`.
---

Interrogate a plan / design until handoff-ready and no high-impact blockers remain.

# BEFORE STARTING
- Ask user: "How many questions do you want?"
  - "15-20 is always solid."
  - "10-15 is still effective."
  - "5-10 for a quick grill."
- Treat selected range as soft budget, not strict quota.
- Never default to minimum of selected range.
- Default targets:
  - `5-10` => `7-8`.
  - `10-15` => `12-13`.
  - `15-20` => `17-18`.
- Example: user sets `5-10`, plan for `7-8` questions unless plan becomes complete sooner or needs more by question `8`.

# START WITH INTENT
- Goal
- Success criteria
- Audience
- Scope boundaries
- Constraints

# AFTER INTENT IS STABLE
- Use hidden completeness frame, track what still matters, such as: interface, data flow, failure modes, UX, rollout, etc.
- Ask next question that removes highest-impact blocker.
- Route questions by blocker severity over following rigid checklist.

# QUESTION SELECTION RULES
- Use selected range as a planning budget, not exact count; Minimum is lower bound, not default target.
  - Pick initial target near midpoint of selected range.
  - Stop before initial target only if intent and implementation are handoff-ready.
  - Reaching initial target should not auto-stop; continue to selected range's top if high-impact blockers remain.
- If question can be answered by exploring code or environment, explore over asking.
- Never ask low-risk detail questions unless detail is likely to distort plan or implementation.
- If something is underspecified, ask unless assumption is low-risk or unlikely to change implementation materially.
- Track resolved decisions; don't repeat or lightly rephrase answered questions.
- Revisit resolved points only if new info creates real inconsistency or invalidates earlier answer.
- Call out weak, inconsistent, or underspecified choices directly.
- Force real tradeoff decision if weak assumption would materially change implementation.
- Never press low-impact disagreements if risk is understood and choice locked.
- Add 🔥 emoji instead of "(recommended)" for most recommended option.

# IF PLAN MODE ACTIVE
- Use `request_user_input` for questions that materially change plan, confirm important assumptions, or choose between real tradeoffs.
- Prefer Codex's clickable question UI over inline `a`/`b`/`c` answer menus.
- Default to 1 high-impact question at a time.
- You may ask 2-3 questions in 1 prompt if are tightly coupled and batching can close a branch faster with less back-and-forth.
- Offer 3-4 meaningful mutually exclusive options.

# IF PLAN MODE INACTIVE OR `request_user_input` UNAVAILABLE
- Fall back to plain-text questions.
- Provide 3-5 concise example answers with letters: `a`,`b`,`c`, etc.
- Keep options short so user can reply like `1a, 2c, 3b`.
- If no answers fit, leave room for freeform answer.

# AFTER 17 QUESTIONS
- Only use this checkpoint if user selected `15-20`.
- Ask "Should we keep going?" with three options: "Keep going", "Stop here", "Three more questions".
  - "Keep going" = continue asking as before.
  - "Stop here" = end questions + produce complete final plan.
  - "Three more questions" = ask three more before asking again.

# WHEN TO STOP
- If no high-impact unresolved blockers remain.
- If top of selected range reached and user has not asked to keep going.
- If user says to stop.

# FINAL OUTPUT
- If questioning is done, produce full handoff-ready `<proposed_plan>` complete on intent, implementation, tests, assumptions, avoid leaving decisions to implementer.
