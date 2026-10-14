---
name: ae-corpus
description: >-
  Index and architecture of the portable Analytics Engineering skill corpus
  (dbt + Looker Studio / Data Studio). Use when choosing which skills to load,
  authoring or refactoring skills, onboarding a teammate to the corpus, or when
  the user asks about skill hierarchy, inheritance, or AE agent documentation.
---

# AE Corpus — index portable

Corpus de skills Cursor pour l’Analytics Engineering, conçu pour être **copié
tel quel** sur chaque machine (`~/.cursor/skills/`). Même corpus → mêmes agents.

Stack ciblée (phase actuelle) : **dbt + Looker Studio (Data Studio)**.

**Frontière portable vs projet :** le corpus publié (repo GitHub / marketplace)
s’arrête à L2 (+ L0/L1 génériques). Toute **mission** (`mission-*`) est
propre à un dépôt : elle vit en local ou dans le monorepo du projet, jamais
dans ce package. Le slot L3 existe pour **n’importe quel** projet.

## Héritage (règle d’or)

```text
Mission  →  ae-dev-gates + plugin dbt  →  tool-* / ae-*
   ↑ deltas locaux     ↑ gates session + savoir dbt officiel
```

1. Un skill **ne répète pas** ce que son parent couvre déjà.
2. Il **pointe** vers le parent (`Lire et appliquer …`) en tête de fichier.
3. En cas de conflit explicite, le skill **le plus bas** (mission / tâche) gagne.
4. Les détails volumineux vont dans des `reference.md` / `project-*.md` lus à la
   demande (progressive disclosure, < 500 lignes pour `SKILL.md`).
5. **Ne pas forker** le plugin dbt : le référencer. Les gates perso vivent dans
   `ae-dev-gates` uniquement.

## Couches

| Couche | Préfixe / nom | Portée | Contenu typique |
|--------|---------------|--------|-----------------|
| L0 Domaine | `ae-*` | Tout projet AE | Modélisation, documentation (hors plugin) |
| L1 Outil | `tool-*` + **plugin dbt** | Stack technique | BigQuery, Looker Studio ; dbt = plugin |
| L2 Gates | `ae-dev-gates` | Tout projet dbt | Ordre de session + gates (pas de reformulation dbt) |
| L3 Mission | `mission-*` | Un dépôt / un projet | Sandbox, conventions, GitLab, interfaces |
| L4 Tâche | sections ou `task-*` | Une routine du projet | Routines métier locales |

`dbt-classic` = **redirigé** vers `ae-dev-gates` (compat liens anciens).

## Catalogue — état actuel

Légende : **OK** · **AMÉLIORER** · **ÉCRIRE** · **ARCHIVER** · **RÉUTILISER** · **DÉPRÉCIÉ**

### L0 — Domaine (à écrire)

| Skill | Statut | Rôle |
|-------|--------|------|
| `ae-data-modeling` | **ÉCRIRE** | Grain, couches, contrats — ce que le plugin ne fige pas pour l’équipe |
| `ae-documentation` | **ÉCRIRE** | YAML / exposures / doc BI — complément au guide officiel |
| `ae-data-testing` | **ÉCRIRE** (v2) | Peut démarrer dans `ae-data-modeling` |

### L1 — Outil

| Skill | Statut | Rôle |
|-------|--------|------|
| Plugin dbt | **RÉUTILISER** | Source de vérité modélisation + CLI |
| `tool-bigquery` | **ÉCRIRE** | Dry-run / seuils coût — extraire des missions locales |
| `tool-looker-studio` | **ÉCRIRE** | Exposures, viz, types LS-friendly |
| Plugin GitLab | **RÉUTILISER** | CI si besoin |
| Omni | **hors scope** | |

### L2 — Gates

| Skill | Statut | Rôle |
|-------|--------|------|
| `ae-dev-gates` | **OK** | Target isolée, cardinalité, lint, coût, Git/MR |
| `dbt-classic` | **DÉPRÉCIÉ** | Redirect → `ae-dev-gates` ; supprimer plus tard |

### L3 — Mission (hors package portable)

Pattern obligatoire pour **tout** projet :

| Élément | Statut | Rôle |
|---------|--------|------|
| `mission-<projet>` | **hors marketplace** | Deltas du dépôt uniquement ; hérite de `ae-dev-gates` + plugin dbt |
| `project-*.md` | **hors marketplace** | Réf. envs / schedules / interfaces, lue à la demande |

Chaque équipe / dépôt fournit sa propre instance. Exemple local non publié :
`dbt-mission` → à renommer `mission-hdi-ae` + `project-hdi.md` (ne pas merger
ici).

### L4 — Tâches

Routines rattachées à **une** mission (hors package). Exemple local non publié :
triage tests, attribution campagnes — à extraire de la mission concernée.

### Orphelins

| Chemin | Statut |
|--------|--------|
| `dbt-lineage/reference.md` | OK annexe |
| `gerard-*`, `michel-*` | **ARCHIVER** |

## Matrice d’héritage cible

```text
ae-corpus                          ← package portable
├── ae-data-modeling / ae-documentation     (L0)
├── tool-bigquery / tool-looker-studio      (L1)
├── plugin dbt (externe)                    (L1)
└── ae-dev-gates                            (L2)

mission-<projet>                   ← hors package (un par dépôt)
├── project-*.md
└── tasks/…                        (L4)
```

En-tête type mission :

```markdown
## Héritage obligatoire

1. [ae-dev-gates](../ae-dev-gates/SKILL.md)
2. Plugin dbt — using-dbt-for-analytics-engineering, running-dbt-commands
3. [tool-bigquery](../tool-bigquery/SKILL.md) si exécution BQ

Ce skill n’ajoute que les deltas ci-dessous.
```

## Quand charger quoi

| Situation | Skills |
|-----------|--------|
| Session dbt générique | `ae-dev-gates` + plugin dbt |
| Dev dans un dépôt avec mission | `mission-<projet>` (tire gates + plugin) |
| Coût / dry-run BQ | `tool-bigquery` |
| Data Studio / viz | `tool-looker-studio` |
| Onboarding corpus | **`ae-corpus`** |

## Portabilité

Repo : marketplace team Converteo (privé sous l’org GitHub).  
Voir [INSTALL.md](INSTALL.md).

## Ordre de construction suivant

1. Écrire L0 (`ae-data-modeling`, `ae-documentation`).
2. Extraire `tool-bigquery`.
3. Écrire `tool-looker-studio`.
4. Côté projets : aligner chaque mission locale sur `mission-*` + L4 (hors repo).
5. Archiver stubs + supprimer `dbt-classic` quand plus aucun lien.
6. Tenir ce catalogue à jour.

## Documentation graphique

Voir [architecture.md](architecture.md).
