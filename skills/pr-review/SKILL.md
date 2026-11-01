---
name: pr-review
description: Review a pull request's diff and report issues ranked P0, P1 and P2, split into blocking and non-blocking. Use when asked to review a PR, review a diff or branch, check changes before merging, or "is this PR ready". Works from a PR number or URL, a branch, a commit range, or a pasted diff.
---

# PR Review

Review the diff, find real problems, rank each one P0, P1 or P2, and report them split into **blocking** and **non-blocking**.

## Severity

| level | meaning | merge |
|---|---|---|
| **P0** | breaks production, loses or corrupts data, opens a security hole, or breaks the build | blocking |
| **P1** | a real bug on a reachable path, a broken contract, a missing migration, or a regression | blocking |
| **P2** | a correctness risk on an edge path, a maintainability or performance problem, or a missing test for new logic | non-blocking |

Blocking means the PR should not merge until it's fixed. Non-blocking means it's worth fixing, but it can land after merge.

Style preferences, naming taste and formatting a linter would catch are not findings. Leave them out. When unsure between two levels, pick the lower one and say why in one line. See `references/severity.md` for examples of each level.

## Steps

### 1. Get the diff

Use whichever of these fits what you were given and what tools you have:

- **PR number or URL:** fetch the diff and the PR description from the code host (for GitHub, `gh pr view <n>` and `gh pr diff <n>`).
- **Branch:** diff against its merge base: `git diff $(git merge-base origin/main HEAD)...HEAD`. Use the repo's real default branch, not an assumed `main`.
- **Pasted diff:** use it as given.

If none of these is available, ask the user for one. Don't guess at what changed.

Read the PR description or linked issue if there is one. It tells you what the change is meant to do, and a diff that doesn't do what it says is a finding.

### 2. Read the context, not only the hunks

A diff hides most bugs. For each changed file, read enough of the surrounding code to know:

- who calls the changed functions, and whether those callers still work
- what the changed types, schemas, configs or APIs are used by
- what the tests cover and what they don't

Skip generated files, lockfiles and vendored code unless the change is in them on purpose.

### 3. Look for problems

Go through the diff with `references/checklist.md`. Cover correctness first, then security, data, contracts, concurrency, performance, and tests.

### 4. Verify each finding

Before reporting a finding, check it against the code:

- Point to the exact line and the exact input or state that triggers it.
- Confirm the path is reachable. If a guard elsewhere already prevents it, drop it.
- If you can't confirm it but it still looks plausible, keep it and mark it **unverified**.

A short list of real findings beats a long list of maybes.

### 5. Report

Use this format. Most severe first within each section. Leave a section out if it's empty.

```markdown
## PR review: <title or ref>

**Verdict:** <Blocked: N blocking issues | Ready to merge | Ready, with N non-blocking notes>

### Blocking

**[P0] <one-line claim>** · `path/to/file.ts:42`
<what goes wrong, with the concrete input or state that triggers it>
**Fix:** <the smallest change that fixes it>

**[P1] ...**

### Non-blocking

**[P2] <one-line claim>** · `path/to/file.ts:88`
<why it matters>
**Fix:** <suggestion>

### Checked and fine
<one or two lines on risky areas you looked at and found no problem, so the reader knows they were covered>
```

## Rules

- Report only. Don't edit code, push commits or post comments to the code host unless the user asks.
- Every finding has a file and line, a concrete failure, and a fix.
- Review the change, not the whole codebase. Mention an existing bug only if the diff makes it worse or depends on it.
- If the diff is too large to review well, say so, review the riskiest files first, and list what you skipped.
