# Sodium for standalone explanations

This skill adapts Sodium's visual language for portable HTML. The bundled starter contains its core light-theme tokens and both font faces, with native HTML recipes for explanations. Use this style on every page produced by `show-me`, including pages about a project with a different design system.

## Visual rules

- White page, warm near-black text, warm off-white panels and code wells. Use the starter's semantic CSS variables for colors and spacing.
- Square corners throughout. Use one thin outline around a region and rules between its parts. Avoid nested boxes, shadows, decorative gradients, blur, and background grids.
- Inter Display at weight 400 for titles and prose. Commit Mono at weight 400 for controls, table headings, labels, code, and identifiers. Distinguish headings by size and spacing rather than bold weight.
- Write sentence case in source. The `.label` role applies mono capitals and tracking together. Keep sentences and headlines in sans, with code in its original case.
- Yellow marks the primary action, selection, or an emphasized data series. Use at most one primary action per group. Links on the light ground use the dark gold `--accent-text`; yellow text and yellow icons on white are unreadable.
- Status colors need a word as well as color. Warning is orange, success green, failure red. If a status needs a mark, use a small square rather than a dot.
- Keep paragraphs within the reading measure. Use compact ruled tables, lists, and diagrams. Several numbers belong in one divided strip rather than separate statistic cards.
- Preserve visible focus indicators. Prefer instant or short state transitions, honor reduced motion, and show the answer immediately.

The starter's 4px spacing scale, 32px controls, 40px table rows, 32px title, 24px heading, and 15px/24px prose come from Sodium's tokens. Layout constraints and diagram geometry may adapt to the explanation; the palette, type roles, corners, and rules stay consistent. The embedded OFL fonts avoid network dependencies; system font stacks remain fallbacks.

## Sources and maintenance

Extracted from the official registry on 2026-11-04:

- [System rules and component index](https://design.how/systems/sodium.md)
- [Theme source, tokens, base styles, and recipes](https://design.how/r/sodium/theme.json)
- [Sodium skill source](https://design.how/r/sodium/skill.json)
- [Frame rules](https://design.how/systems/sodium/components/frame.md)
- [Typography](https://design.how/systems/sodium/foundations/typography.md)
- [Color](https://design.how/systems/sodium/foundations/color.md)
- [Component registry](https://design.how/r/sodium/registry.json)

The upstream shadcn setup, migration skills, and component installation commands apply when building or migrating an application. `show-me` creates a standalone explanation file and does not run them against the host project. Sodium's provided ESLint config targets JS/TS/JSX/TSX, so a plain HTML file is not validated by that command. Check the extracted style rules and browser behavior directly instead of claiming a Sodium lint pass.

When updating the bundled style, consult the current official sources and preserve upstream attribution. The HTML includes design.how's MIT notice and the SIL Open Font License notices for Commit Mono and Inter Display. Keep those notices in generated files.
