---
name: goal
description: "Interrogate long-running Codex work until it can be started as a self-goal with explicit success and stop conditions."
---
# SPEC MODE
If user invoked skill as `$goal implement <file.md>`, don't use `DEFAULT MODE` and instead start a goal using the exact following shape:
`Continually reference <file.md> and implement its slices in order. For each slice: 1. Implement slice; 2. Run validation; 3. Audit full slice THREE times with three separate passes (one pass at a time) with fixes after each pass (don't count minor findings toward audit count); 4. Rerun validation; 5. Audit and update any RELEVANT repo docs/policy surfaces (local AGENTS.md, skills, reference files, etc.) for related drift in two separate passes (one pass at a time) using minimal change (don't audit <file.md> itself); 5. Start next slice and repeat process.`

Before setting goal, read <file.md>. If it only has one slice, edit file to divide contents into relevant/logical sub-slices. Otherwise, leave as is.

# DEFAULT MODE
Design a durable Codex self-goal for the current task.

## DEFAULT OPENING SEQUENCE
`Prompt 1` must batch the depth selector with the first intent question:
- Ask user `How deep should this goal-design pass go?`:
  - `Quick`: core blockers
  - `Standard`: balanced depth
  - `Thorough`: deeper risk scan
- Ask first intent questions in that same prompt: target `work` + `operating context`.

After `Prompt 1`, batch related high-impact questions into each prompt until the objective contract is complete. Prioritize missing success criteria, stop condition, scope/non-goals, and hard constraints.

Depth Target = soft maximum number of user prompts before producing the plan unless a high-impact blocker remains:
- `Quick` => produce plan around prompt `5`
- `Standard` => produce plan around prompt `10`
- `Thorough` => produce plan around prompt `15`

Prompt count tracks user prompts, not raw questions inside prompt. Count opening prompts toward target. Finish early if goal objective is complete and no high-impact blocker remains.

## GOAL OBJECTIVE CONTRACT
A generated goal objective must be compact but complete: enough detail to preserve intent across a long-running task without becoming the implementation plan. Prefer `3-6` short labeled clauses or one concise paragraph with:
1. Desired outcome: what completed work should exist or be true.
2. Relevant context: paths, systems, constraints, user intent, and any known non-goals needed to stay on track.
3. Success condition: concrete evidence that the work is done correctly.
4. Stop condition: when success is reached or when Codex should stop and report a blocker.

- Treat dirty worktree state as pre-goal triage: inspect, classify, and resolve it before `create_goal` when safe to do so. Commit safe relevant work, remove clearly disposable generated state, and stop before `create_goal` only when dirty state is sensitive, destructive to resolve, or impossible to classify.
- Put step-by-step execution details in the `<proposed_plan>`, not in the goal objective.
- The plan's only goal-tool step is `create_goal`; don't add budget or completion-tool steps.

## QUESTION RULES
- If a question can be answered by exploring code, files, or tools, explore over asking.
- Don't ask low risk detail questions unless the answer could materially change goal objective or implementation plan.
- Call out weak or underspecified choices when they would materially weaken the goal objective.
- Always add a fire emoji instead of `(recommended)` directly after the user selectable option you most recommend for each question.
- Prefer `2-3` tightly related questions per prompt when batching reduces back-and-forth without mixing unrelated decisions. Don't batch questions when one answer should shape the next question or when option combinations could conflict.
- Use `request_user_input` for material questions.

## DONE
When questioning done, output `<proposed_plan>` block with:
- clear title
- first implementation step: after user says `Implement plan`, perform any required pre-goal repo/environment triage, then call `create_goal(objective="...")` with compact structured objective only after hard start blockers are resolved
- first work step after goal creation
- scope/non-goals and hard constraints in the objective's `Relevant context`; if too long, include them in a short assumptions section
