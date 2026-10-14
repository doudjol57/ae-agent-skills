# ae-agent-skills

Portable **Analytics Engineering** skills for [Cursor](https://cursor.com) Agent.

Stack focus: **dbt + Looker Studio (Data Studio)**.  
Does **not** include project-specific mission skills (e.g. HDI `dbt-mission`).

Repo: https://github.com/doudjol57/ae-agent-skills

## What's included

| Skill | Role |
|-------|------|
| [`ae-corpus`](skills/ae-corpus/) | Index, inheritance rules, catalog, architecture diagrams |
| [`ae-dev-gates`](skills/ae-dev-gates/) | Session gates: isolated target, join cardinality, lint, cost, MR |

Coming later: `ae-data-modeling`, `ae-documentation`, `tool-bigquery`, `tool-looker-studio`.

## Prerequisites

- Cursor Desktop with Agent Skills
- Official **dbt** plugin (not bundled here — do not fork it)

## Install

### A — Cursor team marketplace (recommended for teams)

1. Push this repo (done) and connect it as a **Team Marketplace**  
   Dashboard → Plugins & MCPs → Add Marketplace → Import from Repo  
   URL: `https://github.com/doudjol57/ae-agent-skills`
2. Teammates install the plugin from **Customize**.
3. Optionally enable **Auto Refresh** on the marketplace.

Requires a Cursor Teams / Enterprise plan.

### B — Local plugin test

```bash
mkdir -p ~/.cursor/plugins/local
ln -sfn "$(pwd)" ~/.cursor/plugins/local/ae-agent-skills
```

Reload Cursor → Customize → confirm skills appear.

### C — Personal skills copy

```bash
git clone https://github.com/doudjol57/ae-agent-skills.git
cp -R ae-agent-skills/skills/* ~/.cursor/skills/
```

## Architecture

See [skills/ae-corpus/architecture.md](skills/ae-corpus/architecture.md) and  
[skills/ae-corpus/SKILL.md](skills/ae-corpus/SKILL.md).

```text
Mission (per project, not in this repo)
  → ae-dev-gates + official dbt plugin
  → tool-* / ae-* (future)
```

## Contributing

- No reformulation of the official dbt plugin — extend via `ae-dev-gates` / new L0–L1 skills.
- Keep each `SKILL.md` under ~500 lines; put detail in sibling markdown files.
- Update `ae-corpus` catalog when adding a skill.
