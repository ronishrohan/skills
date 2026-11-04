---
name: ship-it
description: Ship the current change as a GitHub PR. Review the final diff with pr-review, fix every confirmed finding, commit and push, open or update the PR, document the fixes in comments, and follow GitHub checks. Use when asked to ship it, create a PR, or get a branch ready for review.
---

# Ship it

Take the current work through review, fixes, and a GitHub PR without routine confirmation prompts. GitHub runs the checks. Return the PR URL and its actual CI status.

Adapted from gstack's ship workflow for Ronish's preferences. This file defines the workflow; it does not invoke the upstream skill or its setup, telemetry, local checks, or attribution steps. See [the upstream license](references/gstack-LICENSE.txt).

## 1. Establish the change and base

Read the repository's contribution and PR guidance, relevant issue or plan, and PR template. Inspect the current branch, working tree, commits, and full diff, including untracked files relevant to the task. Keep unrelated work out of staging and the PR.

Determine the GitHub repository and push remote from git remotes. Use the current open PR's base if one exists, otherwise the repository's actual default branch. Do not assume `main`. If there are multiple plausible repositories or targets, clarify the ambiguity rather than pushing to the wrong place.

If on the base/default branch or detached HEAD, create a descriptive feature branch before committing. Continue an existing feature branch when it belongs to this task. Fetch the base and merge it into the feature branch with an ordinary merge. Resolve straightforward conflicts while preserving both changes; stop for conflicts whose intended behavior cannot be determined. Do not discard dirty work to make a merge succeed.

Read `.github/workflows/` to identify which checks should run for this change, including PR event types and path filters. Inspect existing PR comments, review threads, and CI results if this branch already has a PR.

## 2. Finish the change and its documentation

Compare the implementation with the requested outcome. Finish missing in-scope behavior, update documentation affected by the change, and update existing task lists only where the work clearly completes an item. Follow the project's version and changelog policy. Reuse an existing bump; do not invent a VERSION file, four-part version scheme, or release ceremony for a repository that does not use one.

Do not run local tests, lint, typechecks, coverage, evals, verification scripts, or validation builds. Read code and test coverage, and add or update meaningful tests when a fix needs them, but leave execution to GitHub. Do not silently fall back to local checks when CI fails or is missing. This preference overrides repository or inherited skill guidance that asks for local validation, unless a higher-priority instruction requires otherwise.

If commit or push hooks invoke checks, honor the no-local-checks preference using a documented, per-command skip for those check runners when available. Preserve unrelated hooks and protections. Do not change committed hook configuration or broadly disable all hooks to get a commit through. If there is no way to separate mandatory check execution from the git operation, explain the concrete conflict and stop.

## 3. Handle requested screenshots

If the user mentions screenshots, capture and attach the evidence yourself. Read [references/screenshots.md](references/screenshots.md) and complete it before opening the PR. Starting a development server or rendering a page solely for screenshot capture is allowed; it is not permission to run local validation suites.

## 4. Review before opening the PR and fix every finding

Use the `pr-review` skill on the full final change against the fetched base, including this task's uncommitted changes. If it is not available, use the equivalent bundled procedure in [references/pr-review.md](references/pr-review.md). The review reports findings; this shipping workflow owns the edits and subsequent GitHub comments.

Keep a finding ledger with severity, file and line, concrete failure, proposed fix, disposition, and fixing commit. Fix **every confirmed P0, P1, and P2 finding**, including findings described as non-blocking. Severity affects ordering, not whether a confirmed issue gets fixed. Include confirmed findings from existing PR review threads and CI failures.

Investigate unverified findings through code and available evidence. Dismiss a false positive only with a concrete reason; do not count it as fixed. If a finding needs an unresolved product decision or cannot be fixed safely, stop with that exact blocker. Do not quietly defer it or open a ready PR with known unresolved findings.

After fixes, review the resulting diff again, including new tests, documentation, and requested screenshot evidence. Repeat until no confirmed findings remain and the review covers the final content. Re-review after any later code change or base merge. Review by reading the code; do not run local checks as part of the loop.

## 5. Commit and push

Stage named files belonging to this task and make small, logical commits using the repository's conventions. Keep a fix with its relevant tests. Avoid rewriting already published history. Use regular pushes to the feature branch, with upstream tracking on its first push; never force-push or push directly to the base branch through this workflow.

Do not add agent/model co-author trailers, generated-by lines, badges, signatures, or agent attribution to commit messages, the PR title/body, or comments. Keep required source-code licenses and third-party notices intact. Use the user's configured git identity without inventing an identity or removing existing human attribution.

Before pushing, read the staged/published diff for accidental credentials, unrelated files, scratch data, and unintended generated output. This is a manual content review, not a local check command.

## 6. Open or update the PR, then document the fixes

Find an open PR by repository, head owner/branch, and base. Update it if it exists; otherwise create one only after the review-and-fix loop is complete. Use the repository's PR format and a concise title describing the final change. Preserve intentional human-written context when updating an existing body, and re-read it before editing to avoid clobbering concurrent changes.

Lead the description with the user-visible problem and resulting behavior. Include relevant implementation details, requested visual evidence, and a validation section that says **Local checks not run; GitHub Actions handles validation.** Record observed CI results separately. Do not mark test checkboxes passed or claim coverage results based on code inspection.

Write PR bodies and comments to temporary files outside the repository and send those exact files with `gh pr create --body-file`, `gh pr edit --body-file`, or `gh pr comment --body-file`, or equivalent structured tool arguments. Avoid multiline shell interpolation.

Once the PR exists, post a comment documenting the pre-PR findings and fixes. This workflow explicitly authorizes that task-related PR comment and replies to review threads. Use a compact table:

| Severity | Issue and location | Fix | Evidence |
|---|---|---|---|
| P1 | Concrete failure at `path:line` | What changed | Link to the fixing commit or code |

Fill rows only with actual findings. If none were found, say the pre-PR review found no actionable issues. State that execution results come from CI. Reply to existing review threads with the concrete fix and commit link; resolve a thread only when its concern is actually addressed. Do not claim to have fixed unverified or dismissed findings.

On reruns, find and update the previous fix-summary comment rather than posting duplicates. Keep prior fixes in the ledger and add new ones. Use a plain heading such as `Review findings and fixes`, without an agent signature.

## 7. Follow GitHub checks and review feedback

Monitor checks and workflow runs for the PR's **current head SHA**, using GitHub tools or `gh pr checks` and `gh run view` as appropriate. Wait for expected checks to appear and finish. Do not treat an empty checks list, an unrelated run, or a green run on an older commit as a pass. Distinguish intentionally skipped jobs from missing required validation.

For failures caused by this change, read the logs, fix the cause, update relevant tests, repeat the code review, commit, and push. Update the PR comment with the issue, fixing commit, and observed CI outcome. Apply the same process to actionable new review comments. Keep the no-local-checks rule throughout.

If an external dependency, credentials, unavailable runner, permissions, or approval blocks CI, report the exact evidence and what is still pending. Do not label the PR ready. After three fix attempts with the same unexplained failure and no new evidence, stop and report the blocker instead of pushing speculative changes. If the repository has no applicable CI workflow, say validation is unavailable; do not create a workflow or claim success just to complete this step.

## Done

Return the PR URL, a short account of what shipped, the number of confirmed findings fixed, and the observed CI status at the current head. A complete success means all confirmed findings are fixed, requested screenshots are attached, and expected GitHub checks are green or explicitly not applicable. Report a pending or blocked state honestly when that cannot be achieved.

Keep the PR open for review. Merging, publishing releases, and production deployment require a separate user instruction; creating a PR does not authorize those actions. Reruns refresh the review and CI evidence, reuse the branch and PR, and avoid duplicate version bumps, comments, and screenshot uploads.
