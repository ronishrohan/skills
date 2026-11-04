# Screenshot evidence

When the user mentions screenshots, own the capture, upload, and PR formatting. Reuse suitable user-provided evidence when it depicts the exact states, and capture any missing views yourself.

## Capture matching states

- Identify the affected screen and the state that demonstrates the change. Capture the base revision as Before and the final reviewed head as After, using separate temporary worktrees or equivalent isolated checkouts. Preserve the active working tree and use scratch data rather than the user's real app state.
- If the change is still uncommitted, copy this task's changed and new files into the After checkout before rendering. A checkout of HEAD alone would show the old implementation. Refresh the capture after any later review fix that changes the screen.
- Follow the project's run and screenshot instructions. Match viewport, route, theme, zoom, sample data, and interaction state between revisions. Install dependencies and start the app as needed for capture, without running local test/lint/typecheck/eval suites or validation builds.
- Capture the full relevant region at a readable resolution. Show enough context to understand the difference. Hide secrets and private user data before capturing; do not invent or edit pixels to imply a change that was not rendered.
- For a new screen with no meaningful predecessor, provide a clearly captioned After image and explain that it is new. Do not manufacture a Before image. If the base cannot be rendered or the app needs unavailable access, state the exact limitation rather than substituting a mockup.

## Attach actual images

Use an available GitHub asset-upload tool or authenticated browser workflow to upload the screenshots yourself. Verify the resulting images render for the intended repository audience. Local filesystem paths, `file://` URLs, and unexpanded placeholders are not PR attachments.

If no asset uploader is available, use the repository's existing evidence/artifact mechanism. Where the repository permits checked-in screenshot evidence, commit only the requested images under its documented path and reference them with immutable, renderable GitHub URLs pinned to that commit. Do not change repository visibility or upload private evidence to an unrelated public host. If none of these routes is available, report the concrete blocker; do not hand the user an upload chore while claiming completion.

## Format for the PR

Use a table when the views are comparable:

```markdown
## Screenshots

| Before | After |
|---|---|
| ![Before: describe the previous state](BEFORE_IMAGE_URL) | ![After: describe the changed state](AFTER_IMAGE_URL) |

The list now keeps the selected item visible when the panel narrows.
```

Replace the example URLs and caption with actual evidence. For multiple screens, use one labeled pair per screen. If a table makes the images too small, use separate Before and After subsections with full-width images instead. For an After-only capture, use one image and a concrete caption. Prefer useful evidence over a fixed layout.

Re-capture After when a later fix changes the depicted state. Reuse unchanged Before captures and uploaded assets across reruns. Record screenshot capture separately from GitHub's check results; it is visual evidence, not a local test pass.
