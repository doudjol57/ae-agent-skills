# Ideas — backlog AE agent skills

Working backlog for this repo. Not a skill; track work here, then ship via focused MRs.

**Out of scope for this package:** project missions (`mission-*`) and L4 task skills stay in each project repo, never in the marketplace plugin.

## Priorities

| Priority | Theme |
|----------|--------|
| **P0** | English everywhere + README / catalogue / install docs aligned |
| **P1** | Domain skills (L0) + first tool skills (`tool-bigquery`, `tool-data-studio`) |
| **P2** | Broader BI / transform tools (Omni, Power BI, Dataform, SQLMesh) |

---

## P0 — Language & docs sync

### Translate the repo to English

- [x] `plugins/ae-agent-skills/skills/ae-corpus/SKILL.md`
- [x] `plugins/ae-agent-skills/skills/ae-corpus/architecture.md`
- [x] `plugins/ae-agent-skills/skills/ae-corpus/INSTALL.md`
- [x] `plugins/ae-agent-skills/skills/ae-dev-gates/SKILL.md`
- [x] Catalogue legend: use English statuses (`OK` / `WRITE` / `IMPROVE` / `ARCHIVE` / `REUSE` / `DEPRECATED`)
- [x] Policy going forward: **English only** for all skill bodies and corpus docs (README / manifests already EN)

### Adapt the root README

- [x] Reflect multi-tool ambition (not only « dbt + Looker Studio »)
- [x] Clear **shipped vs planned** table (keep in sync with `ae-corpus` catalogue)
- [x] Include `ae-data-testing` in planned skills (today missing from « Coming later »)

### Resynchronize catalogue & diagrams

- [x] `ae-corpus` catalogue: remove Omni out-of-scope; list planned `tool-*` honestly
- [x] `architecture.md`: mark L0/L1 nodes as planned until they exist on disk
- [x] Orphans / `dbt-classic`: local-only / not in package (documented; orphans dropped from published docs)

### Single source of truth for install

- [x] Align root `README.md` and `ae-corpus/INSTALL.md` (Converteo marketplace, `plugins/…` paths)
- [x] Prefer one canonical install path; other file short + pointer

---

## P1 — Missing domain & core tool skills

### L0 — Domain (stubs on disk — expand with AEs)

| Skill | Notes |
|-------|--------|
| `ae-data-modeling` | Grain, layers, contracts — stub shipped |
| `ae-documentation` | YAML / exposures / BI docs — stub shipped |
| `ae-data-testing` | Standalone stub for now; may later fold into modeling |

- [x] Write `ae-data-modeling` (stub)
- [x] Write `ae-documentation` (stub)
- [x] Decide: standalone `ae-data-testing` stub for collaboration (fold later if useful)
- [ ] Expand L0 stubs with AE collaboration (`IMPROVE` → `OK`)

### L1 — Core tools (already in catalogue)

| Skill | Notes |
|-------|--------|
| `tool-bigquery` | Dry-run / cost thresholds — stub (no Cursor marketplace AE plugin) |
| `tool-data-studio` | Exposures, viz, Data Studio–friendly types (was Looker Studio name) |

- [x] Write `tool-bigquery` (stub)
- [x] Write `tool-data-studio` (stub; rename from looker-studio)
- [x] Register each in `ae-corpus` catalogue + architecture
- [x] Bump `plugin.json` / marketplace to `0.3.0`
- [ ] Expand L1 stubs with AE collaboration (`IMPROVE` → `OK`)

---

## P2 — Broader tool skills

Thin AE skills: **do not fork** official Cursor / vendor plugins. Point at them; add AE deltas only (exposures, gates, conventions, when to load).

| Skill | Notes |
|-------|--------|
| `tool-omni` | Wrap / point to Omni Cursor skills + AE deltas |
| `tool-power-bi` | Exposures / semantic model handoff patterns |
| `tool-dataform` | Alternate transform stack vs dbt |
| `tool-sqlmesh` | Alternate transform stack vs dbt |

- [ ] Write `tool-omni`
- [ ] Write `tool-power-bi`
- [ ] Write `tool-dataform`
- [ ] Write `tool-sqlmesh`
- [ ] Update catalogue, architecture, README, `plugin.json` as each lands

---

## Cross-cutting — skill authoring

Apply on every new skill MR (see `ae-corpus/skill-template.md`):

- [x] Document a short **skill template**: inheritance header, YAML frontmatter, under ~500 lines `SKILL.md`, detail in sibling `reference.md`
- [x] Ship **mission-template** (copy-paste L3 kit under `ae-corpus/`; not a loadable marketplace skill)
- [ ] Always update `ae-corpus` catalogue status
- [ ] Always update marketplace `plugin.json` when the packaged surface changes
- [ ] Keep L3/L4 (`mission-*`, tasks) **out** of this repo (template docs OK)

---

## Suggested MR sequence

1. ~~Translation EN + README / catalogue / INSTALL sync (P0)~~
2. ~~Skill authoring template (short doc or section in `ae-corpus`)~~
3. ~~L0 domain skills (stubs)~~ → expand with AEs
4. ~~`tool-bigquery` + `tool-data-studio` (stubs)~~ → expand with AEs
5. ~~Mission bootstrap template (`ae-corpus/mission-template/`)~~
6. P2 tools one MR each (Omni first if Converteo demand is highest)
