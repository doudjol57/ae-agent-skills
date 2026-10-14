# Installer le corpus AE (équipe)

Repo source : https://github.com/doudjol57/ae-agent-skills

Objectif : chaque personne charge le **même** plugin portable.

## Prérequis

- Cursor Desktop avec Agent Skills
- Plugin **dbt** (L1 officiel — obligatoire)

## Bundle portable (ce repo / marketplace)

Uniquement L0–L2 (+ outils génériques). **Aucune** mission projet (`mission-*`).

```text
skills/
├── ae-corpus/             # OK
├── ae-dev-gates/          # OK
├── ae-data-modeling/      # à venir
├── ae-documentation/      # à venir
├── tool-bigquery/         # à venir
└── tool-looker-studio/    # à venir
```

## Install

### Team marketplace

Dashboard → Plugins & MCPs → Import from Repo →  
`https://github.com/doudjol57/ae-agent-skills` → Customize → Install.

### Clone vers skills perso

```bash
git clone https://github.com/doudjol57/ae-agent-skills.git
cp -R ae-agent-skills/skills/* ~/.cursor/skills/
```

### Test plugin local

```bash
ln -sfn /path/to/ae-agent-skills ~/.cursor/plugins/local/ae-agent-skills
```

## Mission projet (hors package)

Chaque dépôt apporte sa propre `mission-*` (local `~/.cursor/skills/` ou
monorepo). Ce package ne la fournit pas.

Installer : **ce plugin** + **la mission du projet**.

## Contribution

- Pas de reformulation du plugin dbt → `ae-dev-gates` + liens plugin.
- Toute mission déclare l’héritage vers `ae-dev-gates`.
- Mettre à jour `ae-corpus/SKILL.md` dans le même changement.
