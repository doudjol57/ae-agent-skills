# Installer le corpus AE (équipe)

Objectif : chaque personne charge le **même** plugin portable via la
**team marketplace** Converteo (privée).

## Prérequis

- Cursor Desktop avec Agent Skills
- Plugin **dbt** (L1 officiel — obligatoire)
- Org Cursor Converteo (Teams / Enterprise)

## Bundle portable (ce repo / marketplace)

Uniquement L0–L2 (+ outils génériques). **Aucune** mission projet (`mission-*`).

```text
.cursor-plugin/marketplace.json
plugins/ae-agent-skills/
└── skills/
    ├── ae-corpus/             # OK
    ├── ae-dev-gates/          # OK
    ├── ae-data-modeling/      # à venir
    ├── ae-documentation/      # à venir
    ├── tool-bigquery/         # à venir
    └── tool-looker-studio/    # à venir
```

## Install

### Team marketplace (recommandé)

1. Repo **privé** sous l’org GitHub Converteo + Cursor GitHub App.
2. Dashboard → Plugins & MCPs → Add Marketplace → Import from Repo.
3. Marketplace Access = groupes Converteo concernés ; Auto Refresh on.
4. Customize → Install **AE Agent Skills**.

### Clone vers skills perso

```bash
git clone <repo-url>
cp -R ae-agent-skills/plugins/ae-agent-skills/skills/* ~/.cursor/skills/
```

### Test plugin local

```bash
cp -R plugins/ae-agent-skills ~/.cursor/plugins/local/ae-agent-skills
```

## Mission projet (hors package)

Chaque dépôt apporte sa propre `mission-*` (local `~/.cursor/skills/` ou
monorepo). Ce package ne la fournit pas.

Installer : **ce plugin** + **la mission du projet**.

## Contribution

- Pas de reformulation du plugin dbt → `ae-dev-gates` + liens plugin.
- Toute mission déclare l’héritage vers `ae-dev-gates`.
- Mettre à jour `ae-corpus/SKILL.md` dans le même changement.
- Nouveau plugin sous `plugins/` → entrée dans `marketplace.json`.
