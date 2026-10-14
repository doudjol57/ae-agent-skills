# ae-agent-skills

Portable **Analytics Engineering** skills for [Cursor](https://cursor.com) Agent.

Stack focus: **dbt + Looker Studio (Data Studio)**.  
Does **not** include project-specific mission skills (`mission-*` — one per repo).

Layout: **Cursor team marketplace** (multi-plugin ready).

```text
.cursor-plugin/marketplace.json   # marketplace manifest
plugins/ae-agent-skills/          # the plugin
  .cursor-plugin/plugin.json
  skills/
```

## What's included

| Skill | Role |
|-------|------|
| [`ae-corpus`](plugins/ae-agent-skills/skills/ae-corpus/) | Index, inheritance rules, catalog, architecture diagrams |
| [`ae-dev-gates`](plugins/ae-agent-skills/skills/ae-dev-gates/) | Session gates: isolated target, join cardinality, lint, cost, MR |

Coming later: `ae-data-modeling`, `ae-documentation`, `tool-bigquery`, `tool-looker-studio`.

## Prerequisites

- Cursor Desktop with Agent Skills
- Official **dbt** plugin (not bundled here — do not fork it)
- Cursor **Teams** or **Enterprise** (for team marketplace)

## Install

### A — Converteo team marketplace (recommended)

1. Host this repo as **private** under the Converteo GitHub org.
2. Install the **Cursor GitHub App** on that org with access to the repo.
3. Dashboard → **Plugins & MCPs** → Team Marketplaces → **Add Marketplace** → **Import from Repo**.
4. Paste the repo URL → confirm plugin `ae-agent-skills` is detected.
5. **Marketplace Settings** → restrict **Marketplace Access** to the right Converteo groups; enable **Auto Refresh**; optionally **Serve marketplace from Cursor**.
6. Set install mode (**Default Off** / **Default On** / **Required**) → Save.
7. Teammates: **Customize** → install from the Converteo marketplace.

### B — Local plugin test

```bash
mkdir -p ~/.cursor/plugins/local
ln -sfn "$(pwd)/plugins/ae-agent-skills" ~/.cursor/plugins/local/ae-agent-skills
```

Reload Cursor → Customize → confirm skills appear.  
(Symlink target must stay **inside** `~/.cursor/plugins/local/` for Cursor to load it — copy instead if symlink is skipped.)

```bash
# Alternative: copy
rm -rf ~/.cursor/plugins/local/ae-agent-skills
cp -R plugins/ae-agent-skills ~/.cursor/plugins/local/ae-agent-skills
```

### C — Personal skills copy

```bash
git clone <repo-url>
cp -R ae-agent-skills/plugins/ae-agent-skills/skills/* ~/.cursor/skills/
```

## Architecture

See [ae-corpus/architecture.md](plugins/ae-agent-skills/skills/ae-corpus/architecture.md) and  
[ae-corpus/SKILL.md](plugins/ae-agent-skills/skills/ae-corpus/SKILL.md).

```text
Mission (per project, not in this repo)
  → ae-dev-gates + official dbt plugin
  → tool-* / ae-* (future)
```

## Contributing

- No reformulation of the official dbt plugin — extend via `ae-dev-gates` / new L0–L1 skills.
- Keep each `SKILL.md` under ~500 lines; put detail in sibling markdown files.
- Update `ae-corpus` catalog when adding a skill.
- Register new plugins in `.cursor-plugin/marketplace.json` if you add another package under `plugins/`.
