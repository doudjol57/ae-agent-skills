---
name: ae-data-modeling
description: >-
  Analytics Engineering modeling guidance: grain, layering, and contracts beyond
  what the official dbt plugin freezes for a team. Use when designing or
  refactoring models, clarifying grain, choosing layers, or defining interfaces.
  Stub — expand with other AEs.
---

# AE Data Modeling

**Status: stub.** Outline for AE collaboration. Fill principles and examples
with the team; do not treat this file as complete guidance yet.

## Inheritance

1. Official dbt plugin (modeling / CLI) when the work is dbt-backed
2. [ae-dev-gates](../ae-dev-gates/SKILL.md) for session order on dbt work

This skill adds only domain guidance below — do not restate the plugin or gates.

## When to use

- Clarifying **grain** and acceptance criteria for a model or mart
- Choosing or reviewing **layers** (staging / intermediate / mart, etc.)
- Defining or changing **contracts** / stable interfaces for downstreams

## Principles / workflow (TODO)

- [ ] Grain: how the team states and validates it
- [ ] Layers: naming and responsibility conventions (portable defaults)
- [ ] Contracts: columns, types, nullability, breaking-change policy
- [ ] Link to [`ae-data-testing`](../ae-data-testing/SKILL.md) for test expectations

## Out of scope

- dbt CLI / `ref()` / selectors → dbt plugin
- Session gates (target, lint, cost, MR) → `ae-dev-gates`
- Project-specific naming or warehouse quirks → `mission-*`
