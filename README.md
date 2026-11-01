# skills

A personal collection of [Claude Code](https://claude.com/claude-code) skills.

## Install

**As a plugin (recommended)** — inside Claude Code:

```
/plugin marketplace add ronishrohan/skills
/plugin install ronish-skills@ronishrohan-skills
```

**Manually** — copy or symlink individual skills into your skills folder:

```sh
git clone https://github.com/ronishrohan/skills.git
ln -s "$PWD/skills/skills/<skill-name>" ~/.claude/skills/<skill-name>
```

## Layout

```
skills/<skill-name>/SKILL.md   # one folder per skill (plus any scripts/references it needs)
template/SKILL.md              # starting point for new skills
.claude-plugin/                # plugin + marketplace manifests
```

## Skills

_None yet._

## Adding a skill

1. `cp -r template skills/<skill-name>` and edit `SKILL.md`.
2. Keep `name` matching the folder name; make `description` say what it does **and** when to trigger.
3. Add a line to the table above and bump `version` in `.claude-plugin/plugin.json`.
