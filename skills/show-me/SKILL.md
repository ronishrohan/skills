---
name: show-me
description: Explain or demonstrate something in a simple Sodium-styled HTML page instead of a long chat response. Use when the user says "show me", asks for a visual explanation, walkthrough, comparison, or demonstration that is clearer with diagrams, images, links, or interaction.
---

# Show me

Put the explanation in a browser page. Use chat for a short handoff with the file link. Every page uses the bundled Sodium style, whatever terminal or chat interface the agent is running in.

## Find what needs showing

Use the user's question and the current conversation to identify what they need to understand or decide. Read relevant code, documents, data, and references before presenting them. If the subject is missing and cannot be inferred, ask for it. Otherwise, proceed.

Examples:

- `/show-me how this authentication flow works`
- `show me the difference between these two approaches`
- `show me what changed and why it matters`
- `show me how to use this feature`

This skill produces an explanation artifact. Creating it does not require migrating the host application's UI or installing a frontend framework.

## Choose a useful presentation

Lead with the answer, then show the evidence or mechanism. Write for the user's level of familiarity. Let the subject determine the page, rather than turning every answer into a dashboard.

| What needs explaining | Useful HTML presentation |
|---|---|
| A sequence or system | Labeled flow, SVG diagram, step-through with an example |
| Alternatives or tradeoffs | Aligned comparison table or side-by-side examples |
| A change | Before and after with annotated screenshots or a visual diff |
| Numbers or cause and effect | Labeled chart, units, and a small interactive example when useful |
| A feature or task | Screenshots, short walkthrough, or a working local demonstration |

Use images, diagrams, video, audio, code, tables, and browser-native interactions when they explain something better than prose. Use only what the subject needs. A compact illustrated explanation is often enough. Avoid pasting a long chat essay into styled containers.

Link to the actual source, file, documentation, or further reading near the statement it supports. Distinguish measured facts, assumptions, illustrative data, and simulated behavior. Use real screenshots for claims about an existing UI. Label generated illustrations and mockups as such. Give images alt text and captions, diagrams readable labels, and charts units and a text or table alternative. Credit third-party media.

## Build with Sodium

Start by copying [assets/page.html](assets/page.html) to a fresh `.show-me/<topic-slug>/index.html`, or to the user's requested location. Resolve the asset relative to this skill's folder, not the working directory. Use a fresh suffix if the destination exists. Replace the example body and document title with the actual explanation. Keep the embedded fonts, license notices, tokens, and shared styles. Load or edit only the relevant part of this large asset; most of its size is embedded fonts.

Read [references/sodium.md](references/sodium.md) before styling. The starter extracts the visual language of [Sodium by design.how](https://design.how/systems/sodium) into plain HTML and CSS. Apply it to the entire artifact, including diagrams and controls. It is a standalone adaptation, not an installation of the React component library.

Keep the page usable directly from `file://` with no server, build step, package install, or runtime CDN. Inline CSS, small scripts, SVG, and required images or other media. Large media may live alongside the HTML if necessary; keep paths relative and hand over the whole folder. External source links remain clickable, but the explanation must remain understandable offline. Use native HTML controls and small local scripts for interaction. Escape code and data before inserting them into HTML; use `textContent` for dynamic text.

For optional detail, prefer `<details>` and anchor links. Add tabs, sliders, zoom, or step controls only when they help the reader understand. Every visible control must work with the keyboard. Keep the main answer visible without running JavaScript. Avoid interactions that call live services or imply a simulated action really happened.

## Check and deliver

If browser inspection is available, check the file at 1280px and 390px, follow its links, and exercise its interactions. Confirm no clipped labels, unreadable diagrams, broken images, missing fonts, or console errors. Keep wide tables and code scrollable within their region. Honor reduced motion and support printing. Acknowledge any verification you could not perform.

Open the finished absolute HTML path in the user's default browser using the available terminal tool:

| OS | Command |
|---|---|
| macOS | `open "$HTML_PATH"` |
| Linux | `xdg-open "$HTML_PATH"` |
| Windows PowerShell | `Start-Process -FilePath $HtmlPath` |

Set the path variable safely for the current shell. If desktop opening is unavailable or fails, provide the file link and open command without claiming it opened. Keep the final chat response to the link and one sentence about what the page shows, plus any material limitation. Put the substantive explanation and citations in the HTML.
