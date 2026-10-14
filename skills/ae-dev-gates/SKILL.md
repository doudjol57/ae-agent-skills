---
name: ae-dev-gates
description: >-
  Thin Analytics Engineering session gates for dbt work: isolated target, join
  cardinality checks, lint before compile, warehouse cost before build, and MR
  structure. Does not restate official dbt plugin skills. Use on every dbt
  modeling or refactor session, or when a mission skill inherits this workflow.
---

# AE Dev Gates

Orchestration + **gates** uniquement. Pour le savoir dbt (modèles, `ref()`,
`dbt show`, sélecteurs, tests, doc), utiliser le **plugin dbt** :
`using-dbt-for-analytics-engineering`, `running-dbt-commands`, et leurs
`references/`.

Une mission projet (ex. HDI) peut durcir ces gates ; en cas de conflit, la
mission prévaut.

## Ordre de session

1. Identifier racine dbt, commande réelle (`dbt` / `uv run dbt` / …), target
   d’écriture isolée — puis `dbt debug`.
2. Clarifier besoin, **grain**, critères d’acceptation (plugin AE + mission).
3. Lire SQL/YAML du sous-graphe ; cartographier avec `dbt list` / plugin.
4. Explorer des données représentatives (`dbt show` — plugin).
5. **Gate cardinalité** sur chaque jointure sensible (ci-dessous).
6. Implémenter (YAML/tests puis SQL — plugin AE).
7. **Gate lint** → compile ciblé.
8. **Gate coût** → puis `dbt build` ciblé uniquement.
9. Valider grain / métier / downstreams.
10. Commit / MR **uniquement** sur demande explicite (**gate Git/MR**).

Ne jamais écrire en production pendant le dev. Ne jamais builder tout le projet
sans accord.

## Gate — target isolée

Écriture uniquement dans une target / schema personnel ou sandbox du projet.
Si aucune n’existe, demander avant toute exécution qui matérialise.

## Gate — cardinalité des jointures

Avant de figer une jointure à risque, mesurer :

- unicité de la clé à **droite** ;
- lignes avant / après ;
- clés avec 0, 1, ou N matches ;
- max de matches pour une ligne source.

Dédupliquer la droite de façon **déterministe** si la clé n’est pas unique.
Préserver les interfaces stables (noms, types, grain) sauf migration acceptée.

## Gate — lint

Si le projet a un linter SQL (ex. SQLFluff) : l’exécuter sur chaque `.sql`
modifié **avant** compile/build. Zéro erreur. Pas d’auto-fix global aveugle.

Puis `parse` / `compile` avec sélecteur précis et
`--warn-error-options '{"error": ["NoNodesForSelectionCriteria"]}'` (voir
`running-dbt-commands`).

## Gate — coût

Avant tout `run` / `build` non trivial :

1. Compiler le sous-graphe ciblé.
2. Dry-run / EXPLAIN entrepôt (détails adapter → skill `tool-*` ou mission).
3. Réduire les scans disproportionnés ; obtenir l’accord si coût notable.

Seuils chiffrés = mission ou `tool-bigquery`, pas ce skill.

## Gate — Git / MR

- Pas de commit, push, ni MR sans demande explicite.
- Retirer config locale / contournements avant commit.
- Description MR **minimale** (trois blocs), adaptée au dépôt :

```markdown
## Changements techniques
### Contexte
### Avant
### Après
### Détail

## Tests et validation
| Étape | Commande / action | Résultat |
|-------|-------------------|----------|
| Lint | | |
| Compile | | |
| Build | | |
| Contrôles données | | |

## Mise en production
1. …
```

Documenter ce qui a **réellement** été exécuté. Une mission peut imposer un
template plus strict (ex. triage tests HDI).

## Checklist courte

```text
- [ ] Target isolée + debug OK
- [ ] Grain et acceptation clairs
- [ ] Plugin dbt appliqué (explore / implémentation)
- [ ] Cardinalités jointures mesurées
- [ ] Lint + compile ciblés
- [ ] Coût estimé puis build ciblé
- [ ] Validation métier
- [ ] Commit/MR seulement si demandés + template respecté
```
