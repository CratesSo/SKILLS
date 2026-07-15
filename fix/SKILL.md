---
name: fix
description: "Use proactively to investigate and fix any known technical issues like bugs, failed tests, regressions, or unexpected behavior. Don't use for code audits/reviews."
---

# Important Rules
- Never implement fixes before investigation.
- If root cause not fully understood, don't speculate, and continue gathering evidence until understood before proceeding.
- You must complete all phases and steps in order:

## Phase 1: Investigate
0. Identify and verify relevant canonical paths.
1. Locate and read any relevant errors, warnings, stack traces, paths, and line numbers.
2. Inspect any relevant recent changes, relevant config, dependencies, and environment differences.
3. For multi-component failures, gather boundary evidence: what enters and exits each component, if config, environment, state, and data propagate correctly.
4. Reproduce issue with exact steps, command, input, or failing test.
5. Trace bad values, state, or behavior backward until source found.

## Phase 2: Compare
1. Locate similar working code or behavior.
2. Compare working and broken paths to identify meaningful differences like config, data, dependency, environment, etc.
3. Stop when enough evidence to form hypothesis.

## Phase 3: Hypothesize
1. State suspected root cause clearly and why evidence supports it.
2. Create smallest useful failing reproduction: automated test, command, script, or manual repro.
3. Test hypothesis with smallest probe or change; If it fails to support hypothesis, discard and return to Phase 1.

## Phase 4: Fix
1. Implement fix.
2. Verify reproduction passes and run narrow validation.

If a fix fails or can't be validated, revert change and return to evidence before trying again.

## Phase 5: Audit
Audits must use a combination of inductive, deductive, causal reasoning, and counterfactual reasoning:
1. Audit fix for correctness three times using three separate passes one at a time, implementing correctness changes after each pass.
2. Run narrow validation.
3. Remove any temp debugging code, tests, or repros.
