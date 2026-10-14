# Project reference — {{project-name}}

Sibling of `mission-{{project-slug}}`. Read **on demand** from the mission skill.
Replace placeholders; rename this file to `project-{{project-slug}}.md`.

## Environments

| Env | Warehouse project / dataset | dbt target | Notes |
|-----|-----------------------------|------------|-------|
| Dev | `{{dev-project}}.{{dev-dataset}}` | `{{dbt-target}}` | Personal or shared sandbox |
| CI | `{{ci-project}}.{{ci-dataset}}` | `{{ci-target}}` | Ephemeral / PR schemas |
| Prod | `{{prod-project}}.{{prod-dataset}}` | `prod` | No local writes |

## Schedules / jobs

| Job | Schedule | Selector / notes |
|-----|----------|------------------|
| `{{job-name}}` | `{{cron-or-trigger}}` | `{{selector}}` |

## Interfaces

| System | Direction | Contract / notes |
|--------|-----------|------------------|
| `{{system}}` | in / out | `{{contract}}` |

## BI / exposures

| Dashboard / report | Tool | Source models / exposures |
|--------------------|------|---------------------------|
| `{{dashboard}}` | Data Studio / Omni / … | `{{models}}` |

## Glossary (project-only)

| Term | Meaning |
|------|---------|
| `{{term}}` | `{{definition}}` |

Keep portable AE vocabulary out of this file — use domain skills instead.
