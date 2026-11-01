# Review checklist

Work through these in order. Skip any that don't apply to the diff.

## Correctness
- Does each changed branch do what it claims for normal, empty, null and boundary inputs?
- Are errors handled, or deliberately passed up, on every new path?
- Do callers of changed functions still get what they expect?

## Security
- Is user input validated and escaped before it reaches SQL, shell, HTML, file paths or URLs?
- Are auth and permission checks present on new endpoints, actions and data reads?
- Are secrets kept out of code, logs and error messages?

## Data
- Do migrations run safely on existing rows, and can they be rolled back?
- Are multi-step writes atomic where they need to be?
- Can a retry or double submit create duplicates?

## Contracts
- Are API responses, event payloads, exported types and config keys backward compatible, or are all consumers updated?
- Are feature flags and env vars defined everywhere the code reads them?

## Concurrency and async
- Can two requests, jobs or renders interleave and leave state wrong?
- Are promises awaited, cancelled and cleaned up?

## Performance
- Any new queries inside loops, unbounded fetches, or work repeated on every render or request?

## Tests
- Does new logic have tests that would fail if it broke?
- Do changed tests still check behavior, or were they weakened to pass?
