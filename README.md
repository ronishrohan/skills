# skills

my personal agent skills. every skill is a plain folder with a `SKILL.md`, following the open [agent skills](https://agentskills.io) format, so they work in any agent that reads it: claude code, cursor, codex, gemini cli, opencode, copilot, and others.

## install

any agent, using the [`skills`](https://github.com/vercel-labs/skills) cli:

```bash
npx skills add ronishrohan/skills                 # pick skills and agents interactively
npx skills add ronishrohan/skills --skill <name>  # just one skill
```

or copy a folder from `skills/` into your agent's skills directory by hand (for example `~/.claude/skills/`, `~/.cursor/skills/`, `~/.codex/skills/`, `~/.agents/skills/`).

as a plugin, where your agent supports one:

```bash
# claude code
/plugin marketplace add ronishrohan/skills
/plugin install skills@ronishrohan
```

## skills

| skill | for |
|---|---|
| [pr-review](./skills/pr-review/SKILL.md) | review a pr diff for p0, p1 and p2 issues, split into blocking and non-blocking |
| [proto](./skills/proto/SKILL.md) | create N distinct design prototypes in one HTML file and open it in your default browser |
| [show-me](./skills/show-me/SKILL.md) | explain or demonstrate something in a Sodium-styled HTML page with diagrams, images, links, and interaction |
| [ship-it](./skills/ship-it/SKILL.md) | review and fix every finding before opening a PR, document the fixes, attach requested screenshots, and leave checks to GitHub |

## layout

```
skills/<name>/SKILL.md   # one folder per skill, plus references/, scripts/, playbooks/ as needed
agents/<name>.md         # subagents, for agents that support them
assets/                  # logo and images
docs/guide/              # longer how-to docs
templates/               # starting points for new skills and agents
plugin.json              # agent-plugins.org manifest
.claude-plugin/, .cursor-plugin/   # thin adapters so those agents can install it as a plugin
```

## add a skill

1. `cp -r templates/skill skills/<name>` and edit `SKILL.md`. keep `name` equal to the folder name.
2. write instructions for any agent: don't assume one agent's tool names or commands.
3. add a row to the skills table above and bump `version` in the three `plugin.json` files.
