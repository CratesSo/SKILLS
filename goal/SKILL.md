---
name: goal
description: "Interrogate long-running Codex work until it can be started as a self-goal with explicit success and stop conditions."
---
Design a durable Codex self-goal for the current task.

## OPENING SEQUENCE

`Prompt 1` must batch the depth selector with the first intent question:
- Ask user `How deep should this goal-design pass go?`:
  - `Quick`: core blockers
  - `Standard`: balanced depth
  - `Thorough`: deeper risk scan
- Ask first intent question in that same prompt: target `work` + `operating context`.

Resolve missing or conflicting `Prompt 1` answers before intent completion. If the request depends on an existing repo, environment, or automation, inspect relevant context first.

After `Prompt 1`, batch related high-impact questions into each prompt until the objective contract is complete. Prioritize missing success criteria, stop condition, scope/non-goals, and hard constraints.

Depth Target = soft maximum number of user prompts before producing the plan unless a high-impact blocker remains:
- `Quick` => produce plan around prompt `5`
- `Standard` => produce plan around prompt `10`
- `Thorough` => produce plan around prompt `15`

Prompt count tracks user prompts, not raw questions inside a prompt. Count opening prompts toward the target. Finish early if the goal objective is complete and no high-impact blocker remains.

## GOAL OBJECTIVE CONTRACT

A generated goal objective must be compact but complete: enough detail to preserve intent across a long-running task without becoming the implementation plan. Prefer `3-6` short labeled clauses or one concise paragraph with:
- Desired outcome: what completed work should exist or be true.
- Relevant context: paths, systems, constraints, user intent, and any known non-goals needed to stay on track.
- Success condition: concrete evidence that the work is done correctly.
- Stop condition: when success is reached or when Codex should stop and report a blocker.

Put step-by-step execution details in the `<proposed_plan>`, not in the goal objective.

The plan's only goal-tool step is `create_goal`; do not add budget or completion-tool steps.

## QUESTION RULES

- If a question can be answered by exploring code, files, or tools, explore over asking.
- Do not ask low risk detail questions unless the answer could materially change the goal objective or implementation plan.
- Call out weak or underspecified choices when they would materially weaken the goal objective.
- Always add a fire emoji instead of `(recommended)` directly after the user selectable option you most recommend for each question.
- Prefer `2-3` tightly related questions per prompt when batching reduces back-and-forth without mixing unrelated decisions. Do not batch questions when one answer should shape the next question or when option combinations could conflict.
- Use `request_user_input` for material questions.

## DONE

When questioning is done, output only one decision-complete `<proposed_plan>` block with:
- clear title
- first implementation step: after the user says `Implement plan`, call `create_goal(objective="...")` with the compact structured objective, then pursue that goal
- first work step after goal creation
- scope/non-goals and hard constraints in the objective's `Relevant context`; if too long, include them in a short assumptions section
