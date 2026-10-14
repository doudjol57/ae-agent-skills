---
name: tool-data-studio
description: >-
  Analytics Engineering deltas for Google Data Studio (also known as Looker
  Studio): exposures, viz-friendly types, and BI handoff. Use when building or
  reviewing Data Studio reports on warehouse models, or documenting exposures.
  Stub — expand with other AEs. No official Cursor Data Studio AE plugin to reuse.
---

# Tool — Data Studio

**Status: stub.** Thin AE wrapper for **Google Data Studio** (product also
marketed as Looker Studio). Fill conventions with the team. No general Cursor
marketplace skill to point at — AE deltas only here.

## Inheritance

1. [`ae-documentation`](../ae-documentation/SKILL.md) for exposures / BI docs
2. [`ae-data-modeling`](../ae-data-modeling/SKILL.md) when grain / contracts feed the report
3. [ae-dev-gates](../ae-dev-gates/SKILL.md) when the session also changes dbt models

This skill adds only AE deltas — not a Data Studio UI tutorial.

## When to use

- Designing or reviewing **Data Studio** reports on curated warehouse tables
- Choosing **viz-friendly types** / naming for BI consumers
- Linking dbt **exposures** to Data Studio assets

## AE deltas (TODO)

- [ ] Preferred semantic types / date handling for Data Studio
- [ ] Exposure pattern (owner, URL, depends_on)
- [ ] What to pre-aggregate in dbt vs calculate in the report

## Out of scope

- Looker (LookML) / other BI products → their own `tool-*`
- Project-specific dashboard inventories → `mission-*` / `project-*.md`
