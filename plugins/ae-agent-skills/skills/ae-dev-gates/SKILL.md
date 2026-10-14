---
name: ae-dev-gates
description: >-
  Thin Analytics Engineering session gates for dbt work: isolated target, join
  cardinality checks, lint before compile, warehouse cost before build, and MR
  structure. Does not restate official dbt plugin skills. Use on every dbt
  modeling or refactor session, or when a mission skill inherits this workflow.
---

# AE Dev Gates

Orchestration + **gates** only. For dbt knowledge (models, `ref()`, `dbt show`,
selectors, tests, docs), use the **dbt plugin**:
`using-dbt-for-analytics-engineering`, `running-dbt-commands`, and their
`references/`.

A project mission (`mission-*`) may tighten these gates; on conflict, the
mission wins.

## Session order

1. Identify dbt root, real command (`dbt` / `uv run dbt` / …), isolated write
   target — then `dbt debug`.
2. Clarify need, **grain**, acceptance criteria (AE plugin + mission).
3. Read SQL/YAML for the subgraph; map with `dbt list` / plugin.
4. Explore representative data (`dbt show` — plugin).
5. **Cardinality gate** on every sensitive join (below).
6. Implement (YAML/tests then SQL — AE plugin).
7. **Lint gate** → targeted compile.
8. **Cost gate** → then targeted `dbt build` only.
9. Validate grain / business rules / downstreams.
10. Commit / MR **only** on explicit request (**Git/MR gate**).

Never write to production during development. Never build the whole project
without agreement.

## Gate — isolated target

Write only to a personal or project sandbox target / schema. If none exists,
ask before any materializing run.

## Gate — join cardinality

Before locking a risky join, measure:

- uniqueness of the key on the **right**;
- row counts before / after;
- keys with 0, 1, or N matches;
- max matches for one source row.

Deduplicate the right side **deterministically** if the key is not unique.
Preserve stable interfaces (names, types, grain) unless a migration is accepted.

## Gate — lint

If the project has a SQL linter (e.g. SQLFluff): run it on every modified
`.sql` **before** compile/build. Zero errors. No blind global auto-fix.

Then `parse` / `compile` with a precise selector and
`--warn-error-options '{"error": ["NoNodesForSelectionCriteria"]}'` (see
`running-dbt-commands`).

## Gate — cost

Before any non-trivial `run` / `build`:

1. Compile the targeted subgraph.
2. Warehouse dry-run / EXPLAIN (adapter details → `tool-*` skill or mission).
3. Shrink disproportionate scans; get agreement if cost is notable.

Numeric thresholds belong in the mission or `tool-bigquery`, not this skill.

## Gate — Git / MR

- No commit, push, or MR without an explicit request.
- Strip local config / workarounds before commit.
- **Minimal** MR description (three blocks), adapted to the repo:

```markdown
## Technical changes
### Context
### Before
### After
### Detail

## Tests and validation
| Step | Command / action | Result |
|------|------------------|--------|
| Lint | | |
| Compile | | |
| Build | | |
| Data checks | | |

## Production rollout
1. …
```

Document what was **actually** run. A mission may require a stricter template
(e.g. local test triage).

## Short checklist

```text
- [ ] Isolated target + debug OK
- [ ] Grain and acceptance clear
- [ ] dbt plugin applied (explore / implement)
- [ ] Join cardinalities measured
- [ ] Targeted lint + compile
- [ ] Cost estimated then targeted build
- [ ] Business validation
- [ ] Commit/MR only if requested + template followed
```
