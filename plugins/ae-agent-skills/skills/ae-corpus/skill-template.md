# Skill authoring template (AE corpus)

Use this when adding or refactoring a portable skill under
`plugins/ae-agent-skills/skills/`. English only. Do **not** put `mission-*` or
L4 tasks in this repo.

## Layout

```text
plugins/ae-agent-skills/skills/<skill-name>/
├── SKILL.md           # required — under ~500 lines
└── reference.md       # optional — detail read on demand
```

## Frontmatter

```markdown
---
name: <skill-name>
description: >-
  <WHAT it does in third person>. Use when <WHEN / trigger terms>.
---
```

- `name`: lowercase, hyphens, max 64 chars; match directory name.
- `description`: WHAT + WHEN; include discovery keywords. Max 1024 chars.

## Body skeleton

Pick the inheritance block that matches the layer. Omit parents that do not apply.

### L0 — domain (`ae-*`)

```markdown
# <Title>

## Inheritance

1. Official dbt plugin (modeling / CLI) when the work is dbt-backed
2. [ae-dev-gates](../ae-dev-gates/SKILL.md) for session order on dbt work

This skill adds only domain guidance below — do not restate the plugin or gates.

## When to use
…

## Principles / workflow
…

## Out of scope
…
```

### L1 — tool (`tool-*`)

```markdown
# <Title>

## Inheritance

1. Vendor / Cursor plugin for this tool (if any) — **do not fork**; link it
2. [ae-dev-gates](../ae-dev-gates/SKILL.md) when the session also runs dbt
3. Domain skills (`ae-*`) when grain / docs / tests apply

This skill adds only AE deltas (cost gates, exposures, conventions, when to load).

## When to use
…

## AE deltas
…

## Out of scope
…
```

### L2 — gates (rare; prefer extending `ae-dev-gates`)

Keep gates thin. Prefer a new section in `ae-dev-gates` over a sibling skill
unless the gate set is truly separate.

### L3 / L4 — not in this package

Do **not** author real missions here. Copy the kit:

→ **[mission-template/](mission-template/)** (`README.md` + `SKILL.md.template` + `project-example.md`)

Ship the filled mission under the **project** repo
(`.cursor/skills/mission-<project>/`) or `~/.cursor/skills/`.

## Rules of thumb

1. Point up; do not copy parent content.
2. Progressive disclosure: procedures in `SKILL.md`; long tables / examples in
   `reference.md`.
3. No fork of official dbt / vendor plugins — reference + AE deltas only.
4. Lowest skill wins on explicit conflict (mission / task over gates / tools).

## MR checklist (every new or changed packaged skill)

- [ ] `SKILL.md` English, frontmatter complete, under ~500 lines
- [ ] Inheritance header present when the skill has parents
- [ ] `ae-corpus` catalog status updated (`WRITE` → `OK`, role text accurate)
- [ ] `architecture.md` / root README shipped-vs-planned table updated if needed
- [ ] `plugins/ae-agent-skills/.cursor-plugin/plugin.json` description / keywords /
      version bumped when the packaged surface changes
- [ ] No `mission-*` or L4 task content in this repo
