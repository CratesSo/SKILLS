---
name: fix
description: "Use proactively for technical fixes: bugs, failed tests, build failures, regressions, performance issues, integration failures, production issues, and unexpected behavior."
---
# Iron Rules
- No fixes before root-cause investigation; Always gather evidence first.
- If root cause is not understood, never propose or apply a fix. 

## Workflow

### Phase 1: Investigate
Complete before suggesting fixes:
1. Read full errors, warnings, stack traces, file paths, line numbers, and error codes.
2. Inspect recent changes, relevant config, dependencies, and environment differences.
3. For multi-component failures, gather boundary evidence before proposing fixes: what enters each component, what exits each component, whether config, environment, state, and data propagate correctly.
4. Reproduce issue with exact steps, command, input, or failing test.
5. Trace bad values, state, or behavior backward until source found.

### Phase 2: Compare
Find the pattern before changing code:
- Locate similar working code or behavior in same codebase.
- Compare working and broken paths.
- Identify meaningful differences, including small config, data, dependency, and environment differences.

### Phase 3: Hypothesize
Use one hypothesis at a time:
- State suspected root cause clearly.
- Explain why evidence supports it.
- Test hypothesis with smallest possible probe or change.
- If it fails, discard hypothesis and return to evidence; Never stack fixes.

### Phase 4: Fix
Fix only after root cause identified:
- Create smallest useful failing reproduction first: automated test, command, script, or manual repro.
- Make one root-cause fix only.
- Verify the reproduction now passes.
- Run narrowest relevant validation for changed behavior.

If two fix attempts fail, stop. Consider if the architecture, pattern, or assumption is wrong before attempting another fix.

## Stop Signal
Return to investigation when you catch any of these:
- proposing fixes without evidence
- proposing fixes before reproducing issue
- proposing fixes before testing hypothesis with smallest probe

If investigation shows an environmental, timing, or external issue, document what was checked and what evidence supports that conclusion. Then add appropriate handling such as retry, timeout, clearer error, or diagnostic logging.
