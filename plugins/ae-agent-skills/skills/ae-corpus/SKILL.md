---
name: ae-corpus
description: >-
  Index and architecture of the portable Analytics Engineering skill corpus
  (dbt, warehouses, BI tools). Use when choosing which skills to load,
  authoring or refactoring skills, onboarding a teammate to the corpus, or when
  the user asks about skill hierarchy, inheritance, or AE agent documentation.
---

# AE Corpus — portable index

Cursor skills corpus for Analytics Engineering. Same corpus on every machine
→ same agent behavior. Ship via the Converteo team marketplace or copy into
`~/.cursor/skills/`.

**Language policy:** skill bodies and corpus docs in this package are **English
only**.

**Current focus:** dbt + Looker Studio (Data Studio), with warehouse/BI tool
skills planned. **Portable vs project boundary:** the published package stops
at L2 (+ generic L0/L1). Any **mission** (`mission-*`) belongs to a project
repo — never in this package. The L3 slot exists for **any** project.

## Inheritance (golden rule)

```text
Mission  →  ae-dev-gates + dbt plugin  →  tool-* / ae-*
   ↑ local deltas     ↑ session gates + official dbt knowledge
```

1. A skill **does not repeat** what its parent already covers.
2. It **points** to the parent (`Read and apply …`) at the top of the file.
3. On explicit conflict, the **lowest** skill (mission / task) wins.
4. Bulky detail goes in `reference.md` / `project-*.md` read on demand
   (progressive disclosure; keep `SKILL.md` under ~500 lines).
5. **Do not fork** the dbt plugin — reference it. Personal gates live only in
   `ae-dev-gates`.

## Layers

| Layer | Prefix / name | Scope | Typical content |
|-------|---------------|-------|-----------------|
| L0 Domain | `ae-*` | Any AE project | Modeling, documentation (beyond the plugin) |
| L1 Tool | `tool-*` + **dbt plugin** | Tech stack | BigQuery, Looker Studio, …; dbt = official plugin |
| L2 Gates | `ae-dev-gates` | Any dbt project | Session order + gates (no dbt rehash) |
| L3 Mission | `mission-*` | One repo / project | Sandbox, conventions, GitLab, interfaces |
| L4 Task | sections or `task-*` | One project routine | Local business routines |

## Catalog — current state

Legend: **OK** · **WRITE** · **IMPROVE** · **ARCHIVE** · **REUSE** · **DEPRECATED**

### L0 — Domain (planned)

| Skill | Status | Role |
|-------|--------|------|
| `ae-data-modeling` | **WRITE** | Grain, layers, contracts — what the plugin does not freeze for the team |
| `ae-documentation` | **WRITE** | YAML / exposures / BI docs — complement official guides |
| `ae-data-testing` | **WRITE** (v2) | May start as a section inside `ae-data-modeling` |

### L1 — Tool

| Skill | Status | Role |
|-------|--------|------|
| dbt plugin | **REUSE** | Source of truth for modeling + CLI |
| `tool-bigquery` | **WRITE** | Dry-run / cost thresholds |
| `tool-looker-studio` | **WRITE** | Exposures, viz, LS-friendly types |
| `tool-omni` | **WRITE** | Point at Omni Cursor skills + AE deltas only |
| `tool-power-bi` | **WRITE** | Exposures / semantic model handoff |
| `tool-dataform` | **WRITE** | Alternate transform stack vs dbt |
| `tool-sqlmesh` | **WRITE** | Alternate transform stack vs dbt |
| GitLab plugin | **REUSE** | CI when needed |

### L2 — Gates

| Skill | Status | Role |
|-------|--------|------|
| `ae-dev-gates` | **OK** | Isolated target, cardinality, lint, cost, Git/MR |

### L3 — Mission (outside portable package)

Required pattern for **every** project:

| Element | Status | Role |
|---------|--------|------|
| `mission-<project>` | **outside marketplace** | Repo deltas only; inherits `ae-dev-gates` + dbt plugin |
| `project-*.md` | **outside marketplace** | Env / schedule / interface refs, read on demand |

Each team / repo provides its own instance. Local unpublished example:
`dbt-mission` → rename to `mission-hdi-ae` + `project-hdi.md` (do not merge here).

### L4 — Tasks

Routines attached to **one** mission (outside package). Local unpublished
examples: test triage, campaign attribution — extract from the relevant mission.

## Target inheritance matrix

```text
ae-corpus                          ← portable package
├── ae-data-modeling / ae-documentation / ae-data-testing  (L0, planned)
├── tool-bigquery / tool-looker-studio / …                 (L1, planned)
├── dbt plugin (external)                                  (L1)
└── ae-dev-gates                                           (L2, shipped)

mission-<project>                  ← outside package (one per repo)
├── project-*.md
└── tasks/…                        (L4)
```

Typical mission header:

```markdown
## Required inheritance

1. [ae-dev-gates](../ae-dev-gates/SKILL.md)
2. dbt plugin — using-dbt-for-analytics-engineering, running-dbt-commands
3. [tool-bigquery](../tool-bigquery/SKILL.md) when running BQ

This skill adds only the deltas below.
```

## When to load what

| Situation | Skills |
|-----------|--------|
| Generic dbt session | `ae-dev-gates` + dbt plugin |
| Dev in a repo with a mission | `mission-<project>` (pulls gates + plugin) |
| Cost / BQ dry-run | `tool-bigquery` (when shipped) |
| Data Studio / viz | `tool-looker-studio` (when shipped) |
| Corpus onboarding | **`ae-corpus`** |

## Portability

Repo: Converteo private team marketplace (GitHub org).  
Install: root [README.md](../../../../README.md) (canonical). Short notes: [INSTALL.md](INSTALL.md).

## Authoring a new skill

Short template (frontmatter, inheritance headers by layer, MR checklist):
[skill-template.md](skill-template.md).

## Build order (next)

1. Write L0 (`ae-data-modeling`, `ae-documentation`; decide `ae-data-testing`).
2. Write `tool-bigquery`, then `tool-looker-studio`.
3. Projects: align each local mission on `mission-*` + L4 (outside this repo).
4. P2 tools one skill at a time (`tool-omni` first if demand is highest).
5. Keep this catalog up to date.

## Diagrams

See [architecture.md](architecture.md).
