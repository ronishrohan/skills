# rstack

my personal stack of agent skills. the same workflows i use every day, packaged so they work in claude code and cursor.

## install

in claude code:

```bash
/plugin marketplace add ronishrohan/skills
/plugin install rstack@ronishrohan-skills
```

claude code prefixes plugin skills, so `/my-skill` becomes `/rstack:my-skill`.

claude code leaves auto-update off for third-party marketplaces. to turn it on, run `/plugin`, open **marketplaces**, select `ronishrohan-skills`, and choose **enable auto-update**. to update by hand: `claude plugin update rstack@ronishrohan-skills`.

## skills

_none yet._

| skill | for |
|---|---|

## agents

_none yet._

## layout

```
rstack/
├── .claude-plugin/plugin.json   # claude code manifest
├── .cursor-plugin/plugin.json   # cursor manifest
├── plugin.json                  # agent-plugins.org manifest
├── skills/<name>/SKILL.md       # one folder per skill, plus references/, scripts/, playbooks/ as needed
├── agents/<name>.md             # subagents
├── assets/                      # logo and images
├── docs/guide/                  # longer how-to docs
└── templates/                   # starting points for new skills and agents
```

## add a skill

1. `cp -r templates/skill skills/<name>` and edit `SKILL.md`. keep `name` equal to the folder name.
2. add a row to the skills table above.
3. bump `version` in all three `plugin.json` files.
