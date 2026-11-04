---
name: proto
description: Create N distinct, interactive design prototypes in one self-contained HTML file and open it in the user's default browser. Use when asked to prototype a design, explore UI directions, compare design variants, or run proto with a brief and a count.
---

# Proto

Turn a design brief into N working prototypes the user can compare in one HTML file. Open the finished file in their default browser.

## Understand the brief

Accept a design description, screenshot, reference, or an existing screen in the current project. Examples:

- `/proto 4 a task manager for a small team`
- `proto this settings page in 3 different directions`
- `use proto to explore a checkout flow`

Use the requested count exactly. If omitted, use 3 and state that assumption briefly. N must be a positive integer. Clarify an invalid or conflicting count before generating. If the design itself is missing and cannot be inferred from the conversation or project, ask for the brief. Otherwise, make reasonable assumptions and proceed.

When working in an existing project, inspect the relevant screen, styles, and assets first. Keep its content, brand constraints, and required behavior unless the user asks to change them. Generate a separate artifact rather than editing production UI.

## Choose distinct directions

Give each direction a short name and a concrete design idea before building. Vary choices that affect the experience, such as layout, information hierarchy, navigation, density, typography, or interaction. Changing only colors or corner radii does not make a new direction.

Use the same task and realistic sample content across variants so the user can compare the designs fairly. Respect any constraints the user wants held constant. For N = 1, build one complete direction without inventing alternatives.

## Build one HTML file

Write `index.html` inside a new `.proto/<brief-slug>/` directory in the working project, or use the user's requested output location. Choose a fresh suffix if the destination already exists. Keep all N prototypes in that single file.

- Embed CSS, JavaScript, icons, and any required assets. The file must work directly from `file://` without a build, server, package install, CDN, or network fetch. Embed needed project assets rather than linking to paths that will break when the file moves.
- Include a compact prototype switcher with a name and one sentence describing each direction. Show one prototype at a time at a useful size. Keep the comparison controls visually separate from the prototype UI. With one prototype, omit the switcher.
- Isolate each variant's styles and state, for example with embedded iframe documents, so switching designs does not cause CSS collisions or leak interaction state.
- Make the main user flow work with local sample data. Buttons, tabs, menus, forms, and dialogs needed to evaluate that flow should respond. Use visible local feedback for simulated actions; do not connect to live services.
- Include desktop and mobile preview widths. Make the preview usable on a narrow browser window, with clear selection state, keyboard-operable controls, readable contrast, and labels for form fields.
- Finish the actual screens with realistic copy and content. Avoid placeholder panels where a core part of the design should be.

## Verify and open

Before handing over, confirm that there are exactly N complete prototypes, all are reachable through the switcher, and the HTML has no missing local dependencies. If browser inspection is available, check each direction, its main interaction, and a narrow viewport. Fix errors you observe. Report any checks you could not run.

Open the absolute HTML path with the operating system's default browser handler. Use the available terminal tool and the command for the current OS:

| OS | Command |
|---|---|
| macOS | `open "$HTML_PATH"` |
| Linux | `xdg-open "$HTML_PATH"` |
| Windows PowerShell | `Start-Process -FilePath $HtmlPath` |

Set the path variable to the actual file using safe shell quoting. Do not select a named browser or substitute an embedded preview for the requested default-browser launch. If the environment cannot open a desktop browser or the command fails, provide the absolute path and the appropriate open command. State the limitation rather than claiming it opened.

Finish with the file link, the number of prototypes, and a brief description of the directions. State whether the browser launch succeeded. Opening a file alone does not count as visual verification.
