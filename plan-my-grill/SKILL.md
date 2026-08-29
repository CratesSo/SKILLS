---
name: plan-my-grill
description: "Build handoff-ready plans through questioning rounds."
---
## OPENING

Seed one internal design tree with the fixed opening rounds. Number every user question continuously from start of interview.

### ROUND 1

Ask exactly these three root questions:
 - `How deep should planning go?`
   - `Quick`: core blockers
   - `Standard`: balanced depth
   - `Thorough`: deeper plan
 - `What outcome should this plan achieve?`: capture the concrete change or end state the user wants
 - `How will we know the result is successful?`: capture observable acceptance criteria that prove the outcome was achieved

### ROUND 2

Ask exactly these three root questions:
 - `Which systems, artifacts, or areas must this plan cover?`: capture positive scope and where responsibility ends
 - `Which related outcomes must be avoided?`: capture explicit non-goals that must not be pulled into the work
 - `What non-negotiable limits or requirements must every solution obey?`: capture hard constraints that restrict the available approaches

## DESIGN TREE

Map every material decision as a lightweight internal node with its prerequisites, the branches it can unlock, and one state: `blocked`, `ready`, `asked`, `tentative`, `settled`.

Represent required environmental evidence as fact prerequisites. Keep the tree in context; don't create or display a separate tree artifact.

Derive branches from the task, settled decisions, and discovered facts. Identify where unresolved choices could materially change this specific plan, then create branches only for those concerns. Relevant concerns may include workflows, interfaces, state, permissions, failure modes, compatibility, rollout, and verification. Treat material edge cases as ordinary decision nodes.

Avoid questions for low-risk details that cannot distort implementation or handoff. Never repeat or lightly rephrase settled questions.

## FRONTIER ROUNDS

At each round boundary:
1. Merge user's complete prior response and every available subagent report.
2. Settle answered decisions and confirmed assumptions. Leave unanswered decisions open.
3. Detect contradictions or changed answers. Reopen affected nodes, invalidate their dependent conclusions, and preserve unaffected branches.
4. Derive any newly relevant branches and prerequisites.
5. Compute the frontier: every open decision whose prerequisites are settled.
6. Rank frontier decisions by implementation risk or cost of ambiguity, then by how many downstream nodes they unlock.
7. Select at most the three highest-ranked decisions as the active frontier; keep other ready nodes queued.

Ask the entire active frontier in one `request_user_input` round, then wait for user response before starting another decision round. A question whose answer depends on any question still open in the current round belongs to a later round.

If no decision is ready because fact prerequisites are still running, wait for the relevant subagent reports and recompute. Pending facts block only their descendants; continue immediately with every unaffected ready decision.

### FACT DISCOVERY

Finding discoverable facts is the agent's responsibility, never user's.

As soon as the tree reveals a needed filesystem, codebase, tool, or environment fact, dispatch a narrowly scoped explorer to find it. Treat the running exploration as an unsettled fact prerequisite. Don't ask user for information that can be discovered from environment.

When a subagent reports, incorporate its evidence at next round boundary. Facts settle evidence nodes; any preference or tradeoff exposed by those facts becomes a user decision.

## QUESTION AND ASSUMPTION RULES

Use `request_user_input` for every decision round (it may also be used for material preferences, tradeoffs, or confirmation of assumptions):
 - Ask no more than three questions.
 - Offer `2-3` meaningful, mutually exclusive options.
 - Mark your most recommended option with `(Recommended)`.

Never settle a material preference or tradeoff without user answer.

Low-risk assumptions may be proposed together in a confirmation round. Keep them `tentative`; they cannot unlock dependent nodes until user confirms them. If rejected, convert affected assumption into open decision and recompute frontier.

Call out weak, inconsistent, or underspecified choices directly when they would materially change implementation. Resolve contradictions before asking questions downstream of them.

## DEPTH AND CONTINUATION

Depth targets count settled user decisions, not prompts or rounds:
 - `Quick`: `12` settled decisions
 - `Standard`: `24` settled decisions
 - `Thorough`: `48` settled decisions

At the selected target, ask `Keep going?` with:
 - `Continue`: keep running frontier rounds
 - `Stop here`: move to completion round
 - `Three more`: settle three more user decisions, then ask `Keep going?` again

## COMPLETION ROUND

If `Stop here` selected, ask `Planning complete: How do you wish to proceed?`, offering in order exactly:
  - `Implement without writing plan`
  - `Write plan only`
  - `Write plan and implement`

If `Implement without writing plan` selected: implement immediately in current task from the in-chat plan.

If `Write plan only` selected: Before creating artifact, ensure current workspace `.gitignore` contains `plans/` and add if absent. Create Markdown plan artifact at `plans/<descriptive-slug>.md` in current workspace; Artifact should cover intent, audience, success criteria, scope, non-goals, hard constraints, locked decisions, confirmed assumptions, implementation, verification, and be detailed enough for unambiguous handoff. Organize implementation as chronological steps based on dependencies, numbered sequentially from `1`, with every step starting with the field `STATUS: NOT STARTED`.

If `Write plan and implement` selected: Follow `Write plan only` workflow. After plan artifact created, use one `request_user_input` round with exactly this question:
 - `Where should the plan be implemented?`:`In this chat`, `New worktree task`, `New local task`

If `In this chat` selected: implement immediately in current task from the plan artifact.

If `New worktree task` or `New local task` selected: use additional `request_user_input` round with exactly these two questions:
 - `Which model should execute the plan?`: `Sol`, `Terra`, `Luna`
 - `Which reasoning effort should be used?`: `Low`, `Medium`, `High`

Create the selected task type immediately with chosen model and reasoning effort. It must receive the plan file path and a concise, self-contained brief instructing it to read the file fully and implement the plan.
