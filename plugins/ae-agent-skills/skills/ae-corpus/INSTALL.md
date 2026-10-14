# Install AE corpus (short)

**Canonical install instructions:** root [README.md](../../../../README.md)
(sections *Install* A / B / C).

## Prerequisites

- Cursor Desktop with Agent Skills
- Official **dbt** plugin (L1 — required; not bundled here)
- Cursor **Teams** / **Enterprise** for the Converteo team marketplace

## What this package ships

L0–L2 portable skills only. **No** project missions (`mission-*`).

| Status | Skills |
|--------|--------|
| Shipped | `ae-corpus`, `ae-dev-gates` |
| Stub (expand with AEs) | `ae-data-modeling`, `ae-documentation`, `ae-data-testing`, `tool-bigquery`, `tool-data-studio` |
| Planned | `tool-omni`, `tool-power-bi`, `tool-dataform`, `tool-sqlmesh` |

```text
.cursor-plugin/marketplace.json
plugins/ae-agent-skills/
└── skills/
    ├── ae-corpus/           # shipped
    ├── ae-dev-gates/        # shipped
    ├── ae-data-modeling/    # stub
    ├── ae-documentation/    # stub
    ├── ae-data-testing/     # stub
    ├── tool-bigquery/       # stub
    └── tool-data-studio/    # stub
```

## Quick paths

| Path | Where |
|------|--------|
| Team marketplace | README → *Install A* |
| Local plugin test | README → *Install B* |
| Personal `~/.cursor/skills/` copy | README → *Install C* |

## Project mission (outside package)

Install: **this plugin** + **one `mission-<project>` per repo**.

Missions are not in the marketplace. Bootstrap from the copy-paste kit:

[mission-template/README.md](mission-template/README.md)

```text
# Preferred layout in the project repo
.cursor/skills/mission-<project>/
├── SKILL.md                 # from SKILL.md.template — deltas + inheritance
├── project-<project>.md     # envs / schedules / interfaces
└── tasks/…                  # optional L4 routines
```

Every mission must keep the **Required inheritance** block pointing at
`ae-dev-gates`, the dbt plugin, and any relevant `tool-*` / `ae-*`.

## Contribution

- Do not restate the dbt plugin → `ae-dev-gates` + plugin links.
- Every mission declares inheritance to `ae-dev-gates` (use mission-template).
- Update `ae-corpus/SKILL.md` in the same change when the portable surface changes.
- New plugin under `plugins/` → entry in `marketplace.json`.
- Skill bodies and corpus docs: **English only**.
- Do not add real `mission-*` skills under `plugins/…/skills/` — template only.
