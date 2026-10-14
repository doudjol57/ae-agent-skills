# Bootstrap a project mission (L3)

Copy-paste kit for a **project-specific** skill. Not a Cursor skill by itself —
this folder lives under `ae-corpus` so the marketplace does **not** auto-load it.

## Prerequisites

1. Install the portable package (Converteo marketplace or local plugin).
2. Official **dbt** plugin installed in Cursor.
3. A project repo where the mission will live.

## Where to put the mission

Pick **one** location per project:

| Location | When |
|----------|------|
| `<repo>/.cursor/skills/mission-<project>/` | Preferred — travels with the repo |
| `~/.cursor/skills/mission-<project>/` | Personal / single-machine only |

## Steps

1. Copy this folder’s contents into the target path and rename:

   ```bash
   # Example: repo-local skill
   PROJECT=my-client   # short slug, lowercase, hyphens
   DEST="<repo>/.cursor/skills/mission-${PROJECT}"
   mkdir -p "$DEST"
   cp SKILL.md.template "$DEST/SKILL.md"
   cp project-example.md "$DEST/project-${PROJECT}.md"
   ```

   The source file is named `SKILL.md.template` on purpose so Cursor never
   auto-loads this kit as a skill.

2. Edit the new `SKILL.md`:
   - Replace every `{{PLACEHOLDER}}`
   - Fill **Project deltas** only (sandbox, GitLab, interfaces, conventions)
   - Keep the **Required inheritance** block; trim tool lines you do not use
   - Do **not** copy text from `ae-dev-gates` or the dbt plugin

3. Edit `project-<project>.md` with envs, schedules, and interface notes.
   Link it from the mission body under *Project references*.

4. Optional L4: add `tasks/<routine>.md` (or sections) for project-only routines.
   Point to them from the mission; keep each file short.

5. Reload Cursor → confirm `mission-<project>` appears under Agent Skills.

## Checklist (before first use)

- [ ] `name:` in frontmatter is `mission-<project>` and matches the folder name
- [ ] `description:` includes project name + discovery keywords (dbt, repo, stack)
- [ ] **Required inheritance** lists `ae-dev-gates` + dbt plugin (+ relevant `tool-*` / `ae-*`)
- [ ] Body states: *This skill adds only the deltas below*
- [ ] No restated gate / modeling / CLI content from parents
- [ ] Bulky tables live in `project-*.md`, not in `SKILL.md`
- [ ] Teammates install **marketplace package + this mission**

## Inheritance reminder

Cursor does not execute a real `extends`. Reliability comes from:

1. Marketplace skills present on the machine
2. Explicit “Read and apply …” pointers in the mission
3. Agent loading the mission first (good `description` / triggers)

On conflict, the mission (or L4 task) wins over gates / tools.
