---
name: goal
description: "Interrogate long-running Codex work until it can be started as a self-goal with explicit success and stop conditions."
---
# SPEC MODE
If user invoked skill as `$goal implement <file.md>`, skip `DEFAULT MODE` and instead start a goal using exact shape:
`Continually reference <file.md> and implement its slices in order. For each slice: 1. Implement slice; 2. Audit slice for correctness with three separate consecutive reviewer passes one at a time with fixes after each pass; 3. Audit any RELEVANT repo docs/policy surfaces (local AGENTS.md, repo local skills, reference files, docs, etc.) for drift or correctness in relation to recent implementation with two separate consecutive passes using minimal change (don't audit <file.md> itself); 4. Start next slice and repeat process.`

Read <file.md> before setting goal; If file has one or no obvious slices, edit contents into logical and efficient chronological implementation slices. Otherwise, leave as is.

# DEFAULT MODE
Question user so you can design a durable Codex goal objective to call the goal tool with.

## PROMPT 1
`Prompt 1` must batch depth selector with first intent questions:
- Ask user `How deep should this goal go?`:
  - `Quick`: core blockers
  - `Standard`: balanced depth
  - `Thorough`: deeper risk scan
- Ask first two intent questions in that same prompt: target `work` + `operating context`.

### Depth Target
Prompt count tracks user prompts, not raw questions inside prompt. Finish early or later depending on if goal objective is complete with no high-impact blockers, edge-cases, or ambiguity remaining.
- `Quick`: produce plan around prompt `5`
- `Standard`: produce plan around prompt `10`
- `Thorough`: produce plan around prompt `15`

## GOAL OBJECTIVE CONTRACT
- After `Prompt 1`, batch related high-impact questions into each prompt until objective contract complete. Prioritize missing success criteria, stop condition, scope/non-goals, and hard constraints.
- A generated goal objective must be compact but complete: enough detail to preserve intent across a long-running task without becoming the implementation plan.
- Prefer `4-6` short labeled clauses or one concise paragraph with:
  1. Desired outcome: what completed work should exist or be true.
  2. Relevant context: paths, systems, constraints, user intent, and any known non-goals needed to stay on track.
  3. Success condition: concrete evidence that work is done correctly.
  4. Stop condition: when success is reached or when Codex should stop and report blocker.

## QUESTION RULES
Use `request_user_input` as the default questioning mode for material questions:
- If question can be answered by exploring code, files, or tools, explore over asking.
- Don't ask low risk detail questions unless answer could materially change goal objective or implementation plan.
- Call out weak or underspecified choices when they would materially weaken goal objective.
- Mark the user-selectable option you most recommend with `(Recommended)`.
- Prefer `2-3` tightly related questions per prompt when batching reduces back-and-forth without mixing unrelated decisions. Don't batch questions when one answer should shape the next question or when option combinations could conflict.

## DONE
1. When questioning done, output `<proposed_plan>` block containing designed goal objective in fenced block.
2. When user says `Implement plan`, call `create_goal(objective="...")` with structured objective only; don't add budget or completion-tool steps.
