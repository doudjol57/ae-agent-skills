---
name: ae-data-testing
description: >-
  Analytics Engineering data testing guidance: which tests to apply at which
  layer, and how that complements official dbt testing docs. Use when adding or
  reviewing tests, choosing severity, or defining quality bars for models. Stub
  — expand with other AEs; may later fold into ae-data-modeling.
---

# AE Data Testing

**Status: stub.** Standalone skeleton so AEs can collaborate here. Decision
open: keep separate or fold into [`ae-data-modeling`](../ae-data-modeling/SKILL.md)
once content stabilizes.

## Inheritance

1. Official dbt plugin (tests / unit tests) when the work is dbt-backed
2. [ae-dev-gates](../ae-dev-gates/SKILL.md) for session order on dbt work
3. [`ae-data-modeling`](../ae-data-modeling/SKILL.md) for grain and contracts under test

This skill adds only testing guidance — do not restate the plugin or gates.

## When to use

- Choosing **generic vs custom** tests for a model
- Setting a **quality bar** by layer (staging vs mart)
- Reviewing failing or noisy tests with the team

## Principles / workflow (TODO)

- [ ] Default tests by layer / grain
- [ ] When to use unit tests vs data tests
- [ ] Severity, quarantine, and known-bad-row patterns (portable defaults only)
- [ ] Link back to modeling contracts

## Out of scope

- Exact dbt test YAML syntax / selectors → dbt plugin
- Project-specific triage routines → `mission-*` / L4 tasks
