# AE Corpus — documentation graphique

## Vue top → bottom

```mermaid
flowchart TB
  subgraph L0 [L0 Domaine]
    ADM[ae-data-modeling]
    ADOc[ae-documentation]
  end

  subgraph L1 [L1 Outil]
    TBQ[tool-bigquery]
    TLS[tool-looker-studio]
    PDBT[Plugin dbt officiel]
  end

  subgraph L2 [L2 Gates]
    GATES[ae-dev-gates]
  end

  subgraph L3 [L3 Mission HDI — hors marketplace]
    MH[dbt-mission / mission-hdi-ae]
    PH[project-hdi.md]
  end

  subgraph L4 [L4 Tâches]
    T1[sales-test-triage]
    T2[attribution-ga4]
  end

  PDBT -.->|savoir dbt ne pas forker| GATES
  ADM --> GATES
  ADOc --> GATES
  TBQ --> GATES
  GATES --> MH
  TBQ --> MH
  TLS --> MH
  PDBT --> MH
  PH --> MH
  MH --> T1
  MH --> T2
```

## Flux d’une session

```mermaid
flowchart LR
  Q[Demande] --> IDX{ae-corpus}
  IDX -->|HDI| M[dbt-mission]
  IDX -->|générique| G[ae-dev-gates]
  M --> G
  G --> P[Plugin dbt]
  G --> Tool[tool-bigquery / LS]
  M --> Task{Tâche L4?}
  Task -->|oui| L4[task file]
  Task -->|non| Impl[Deltas mission]
  L4 --> Impl
  Impl --> Out[Lint coût build MR]
```

## Remplacement de dbt-classic

```mermaid
flowchart LR
  subgraph before [Avant]
    DC[dbt-classic 300 lignes]
    OFF1[Plugin dbt]
    DC -.->|doublon| OFF1
  end

  subgraph after [Après option B]
    AG[ae-dev-gates mince]
    OFF2[Plugin dbt]
    REDIR[dbt-classic redirect]
    AG -->|délègue savoir| OFF2
    REDIR --> AG
  end
```

## Périmètre phase actuelle

```mermaid
mindmap
  root((AE Corpus portable))
    In portable package
      Plugin dbt externe
      ae-dev-gates
      ae-corpus
      tool-bigquery
      tool-looker-studio
      L0 domaine
    Hors package
      Mission HDI
      project-hdi.md
      Ingestion
      Omni
      dbt-classic contenu
```
