---
name: tool-bigquery
description: >-
  Analytics Engineering deltas for Google BigQuery: dry-run / cost awareness and
  warehouse conventions used with dbt. Use when estimating query cost, dry-running
  SQL, or setting BigQuery-specific thresholds. Stub — expand with other AEs. No
  official Cursor BigQuery AE plugin to reuse; do not fork vendor docs.
---

# Tool — BigQuery

**Status: stub.** Thin AE wrapper. Fill cost thresholds and conventions with the
team. There is no general Cursor marketplace BigQuery AE skill to point at —
keep this file as the portable home for our deltas only.

## Inheritance

1. Official dbt plugin when the session runs dbt
2. [ae-dev-gates](../ae-dev-gates/SKILL.md) for session order (cost gate calls this skill)
3. Domain skills (`ae-*`) when grain / docs / tests apply

This skill adds only AE deltas — not a BigQuery tutorial.

## When to use

- Dry-run / bytes-billed estimates before `dbt build` / ad-hoc SQL
- Agreeing **cost thresholds** (portable defaults; missions may tighten)
- BigQuery-specific modeling notes that are not project-only

## AE deltas (TODO)

- [ ] How to dry-run (bq CLI / console / dbt adapter patterns the team uses)
- [ ] Default cost / bytes thresholds and when to ask before running
- [ ] Partition / cluster reminders that belong in portable AE guidance

## Out of scope

- Full BigQuery admin / IAM / slot management
- Project sandbox dataset names → `mission-*`
- Generic dbt modeling → dbt plugin + `ae-data-modeling`
