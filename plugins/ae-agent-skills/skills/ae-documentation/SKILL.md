---
name: ae-documentation
description: >-
  Analytics Engineering documentation guidance: YAML descriptions, exposures,
  and BI-facing docs that complement official dbt guides. Use when writing or
  reviewing model/column docs, exposures, or handoff notes for BI tools. Stub —
  expand with other AEs.
---

# AE Documentation

**Status: stub.** Outline for AE collaboration. Fill standards and examples
with the team; do not treat this file as complete guidance yet.

## Inheritance

1. Official dbt plugin (docs / YAML) when the work is dbt-backed
2. [ae-dev-gates](../ae-dev-gates/SKILL.md) for session order on dbt work
3. [`ae-data-modeling`](../ae-data-modeling/SKILL.md) when grain / contracts drive the docs

This skill adds only documentation guidance — do not restate the plugin or gates.

## When to use

- Writing or reviewing **model / column YAML** descriptions
- Defining **exposures** (dashboards, notebooks, pipelines)
- Documenting handoff for **BI / semantic** consumers

## Principles / workflow (TODO)

- [ ] Minimum bar for model and column descriptions
- [ ] Exposure patterns (owners, maturity, depends_on)
- [ ] What belongs in dbt docs vs BI tool vs mission `project-*.md`
- [ ] Cross-link to `tool-looker-studio` / other BI skills when they exist

## Out of scope

- Full dbt docs site / codegen → dbt plugin
- Tool-specific viz settings → `tool-*`
- Project glossary or stakeholder maps → `mission-*`
