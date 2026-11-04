# Pre-PR review

Use this when the standalone `pr-review` skill is unavailable. It follows the same P0/P1/P2 review procedure. The parent ship-it workflow fixes all confirmed findings, including P2, before PR creation.

1. Read the task, linked issue or plan, and entire change against the fetched base. Include task-related staged, unstaged, and untracked changes; a three-dot commit diff alone omits them.
2. Read enough surrounding code to trace changed functions through callers, schemas, configuration, and consumers. Inspect tests by reading them. Do not execute checks locally.
3. Work through [the checklist](checklist.md). Report only problems with a concrete failure or maintenance cost in the changed behavior. Skip naming preferences, formatter output, speculative future requirements, and unrelated existing bugs.
4. For each finding, identify file and line, triggering input or state, reachability, and the smallest fix. Drop a finding when a guard already prevents the failure. Label a plausible but unconfirmed concern as unverified until investigated.
5. Rank findings using [the severity examples](severity.md). P0 covers security, data loss, production outages, or a broken build; P1 covers reachable bugs, regressions, and broken contracts; P2 covers concrete edge cases, missing behavioral coverage, performance risks, and maintainability defects.
6. Report blocking P0/P1 findings first, then non-blocking P2 findings, followed by a brief account of risky areas reviewed without findings. A clean code review means no actionable code findings remain; it does not imply tests ran or the PR is ready to merge.

Keep every finding in the parent's ledger until fixed or disproved with evidence. If the diff is too large for one pass, divide it by subsystem and account for every part before calling the review complete.
