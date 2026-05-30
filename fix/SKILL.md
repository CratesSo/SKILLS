---
name: fix
description: "Use proactively for any technical fixes like bugs, failed tests, build failures, regressions, performance issues, production issues, and unexpected behavior."
---
# Iron Rules
- Never implement fixes before investigation.
- If root cause not understood, don't speculate; continue gathering evidence until understood before proceeding.

## Workflow
You must complete all phases below in order and their subsequent steps in order:

### Phase 1: Investigate
1. Read any relevant errors, warnings, stack traces, paths, and line numbers.
2. Inspect any relevant recent changes, relevant config, dependencies, and environment differences.
3. For multi-component failures, gather boundary evidence: what enters and exits each component, if config, environment, state, and data propagate correctly.
4. Reproduce issue with exact steps, command, input, or failing test.
5. Trace bad values, state, or behavior backward until source found.

### Phase 2: Compare
1. Locate similar working code or behavior.
2. Compare working and broken paths.
3. Identify meaningful differences like config, data, dependency, environment, etc.
4. Stop when you have enough evidence to form hypothesis.

### Phase 3: Hypothesize
Focus on one highest confidence hypothesis at a time:
1. State suspected root cause clearly and why evidence supports it.
2. Create smallest useful failing reproduction: automated test, command, script, or manual repro.
3. Test hypothesis with smallest probe or change; If it fails, discard hypothesis and return to evidence.

### Phase 4: Fix
1. Implement root-cause fix.
2. Verify reproduction passes and run validation.
3. Audit fix for correctness and implement correctness changes.
4. Audit fix for correctness a second time and implement correctness changes.
5. Audit fix for correctness a third time and implement correctness changes.
6. Run narrowest validation.
7. Remove any temporary debugging code, tests, or repros.
8. Fix any potential docs/policy surface drift with minimal change.

Perform audits one at a time; after correctness changes, move to next audit.

- If a fix fails or can't be validated, revert change and return to evidence before attempting again.
- If two fix attempts on the same issue fail, stop and consider if the architecture, pattern, or assumption is wrong and proceed with a different approach.
- If investigation showed environmental, timing, or external issue, state what was checked and what evidence supports that conclusion and add appropriate handling like retry, timeout, clearer error, diagnostic logging, etc.
