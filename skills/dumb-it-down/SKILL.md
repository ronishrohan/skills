---
name: dumb-it-down
description: Explain concepts, compare options or research findings, and report task or optimization results in plain language with simple tables. Use for "explain simply", "how is A different from B", "show before and after", "what improved", or summaries covering several items.
---

# Dumb it down

Make the answer easy to understand and compare. Lead with the main finding in one or two sentences, then use a simple Markdown table for comparisons, before/after results, or two or more items.

## Do the work, then explain it

Complete the requested research, changes, or measurements before reporting the result. This skill shapes the explanation. It does not replace the task with a summary or change what the user authorized.

Use the user's question to choose the rows and columns. Keep requested detail and deliverables. An explicit request for another format takes priority.

## Choose the table

Use the smallest set of columns that answers the question. These are starting points, not mandatory templates.

| Task | Useful columns |
|---|---|
| Compare A and B | Aspect / A / B / Why it matters |
| Report an optimization | Metric / Before / After / Change |
| Explain a behavior change | Area / Before / After / Effect |
| Summarize research | Finding / Evidence / What it means |
| Report on several items | Item / Result / Next step |
| Explain several concepts | Concept / Plain meaning / Example |

For an A/B comparison, put the same aspect in each row so the reader can compare directly. For separate items, give each item its own row. Include every requested item, including failures and unfinished work.

For a single simple fact or concept, a short explanation is enough. For a process that needs an ordered sequence, keep the sequence and use a table only where it helps compare items.

## Keep tables easy to read

- Use concrete column names, such as the actual product names or "Page load time".
- Keep cells to a short phrase or sentence. Use plain words and explain necessary technical terms once.
- Include columns only when they add useful information. Split a wide table into smaller tables by topic.
- Keep long explanations, code, and procedures outside cells. Add only the detail needed to understand the table.
- Put the main differences or most consequential results first. Avoid repeating the table in prose below it.

## Keep the evidence clear

For research, verify claims against relevant sources and link evidence beside the claim, in the cell or immediately below the table. Distinguish sourced facts from your own conclusions. State unknowns as "Unknown" or "Not verified" instead of guessing. Include a date or version when it changes the comparison.

For optimization results, use comparable measurements with units. State the test conditions and number of runs briefly below the table. Say whether a lower or higher value is better. Compute changes from the recorded values and label them clearly, such as "25% less time". Use percentage points for differences between percentages. Report regressions as clearly as improvements.

If a baseline or measurement is missing, write "Not measured" in that cell. Describe observed behavior separately from measured improvements. Never turn an estimate or a successful test into a measured speedup.

## Apply Poteto's /unslop

Before sending the answer, read and apply the bundled [Poteto /unslop rules](references/unslop.md). They ship with this skill so a separate plugin installation is unnecessary.

Edit the introduction, headers, cells, and any follow-up text. Prefer familiar words, short sentences, and concrete facts. Preserve technical meaning, qualifications, measurements, and source links while simplifying the wording.

Finish when the user can see the answer and compare the requested items without decoding jargon or reading the same information twice. Add a recommendation or next step only when it helps answer the request.
