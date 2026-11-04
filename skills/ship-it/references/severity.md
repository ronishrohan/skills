# Severity examples

## P0, blocking
- SQL, shell or HTML built from user input without escaping.
- A secret, token or private key committed in the diff.
- An auth or permission check removed, bypassed or applied to the wrong resource.
- A migration that drops or rewrites data with no backfill or rollback.
- A change that fails to compile, fails type checks, or crashes on startup.
- An infinite loop, unbounded retry, or unbounded memory growth on a common path.

## P1, blocking
- A logic error on a normal path: wrong condition, off-by-one, inverted flag, wrong variable.
- An unhandled error or null on a path that real input reaches.
- A changed function signature, API response, event shape or config key whose callers weren't updated.
- A race between concurrent requests, jobs or async UI updates that gives wrong results.
- A schema change without its migration, or code that assumes a migration has already run.
- Behavior that doesn't match what the PR description or linked issue says it should do.
- A regression in an existing feature.

## P2, non-blocking
- An edge case that's possible but rare (empty list, timezone boundary, very large input).
- New logic with no tests, or tests that check the implementation instead of the behavior.
- An N+1 query, repeated work in a loop, or a missing index on a path that isn't hot yet.
- Duplicated logic that will drift, or an abstraction that makes the next change harder.
- Error messages or logs that would make a production failure hard to diagnose.
- Dead code or a leftover debug statement.

## Not findings
- Naming, formatting or style that a linter or formatter covers.
- "I would have done it differently" with no concrete cost.
- Speculation about future requirements.
