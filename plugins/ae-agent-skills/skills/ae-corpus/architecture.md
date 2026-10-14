# AE Corpus — architecture diagrams

L0 and core L1 (`tool-bigquery`, `tool-data-studio`) are **stubs** on disk.
Other L1 `tool-*` remain planned. `ae-corpus` and `ae-dev-gates` are complete for v0.

## Top → bottom view

```mermaid
flowchart TB
  subgraph L0 [L0 Domain — stubs]
    ADM[ae-data-modeling]
    ADOc[ae-documentation]
    ADT[ae-data-testing]
  end

  subgraph L1 [L1 Tool — stubs + planned + external]
    TBQ[tool-bigquery]
    TDS[tool-data-studio]
    TOM[tool-omni / PBI / …]
    PDBT[Official dbt plugin]
  end

  subgraph L2 [L2 Gates — shipped]
    GATES[ae-dev-gates]
  end

  subgraph L3 [L3 Mission — outside marketplace]
    MH[mission-project]
    PH[project-ref.md]
  end

  subgraph L4 [L4 Tasks — outside marketplace]
    T1[task-a]
    T2[task-b]
  end

  PDBT -.->|dbt knowledge — do not fork| GATES
  ADM --> GATES
  ADOc --> GATES
  TBQ --> GATES
  GATES --> MH
  TBQ --> MH
  TDS --> MH
  TOM --> MH
  PDBT --> MH
  PH --> MH
  MH --> T1
  MH --> T2
```

L3 / L4 are **slots**: each repo owns its mission (`mission-*`) and tasks.
The portable package does not contain them. Bootstrap kit (docs only, not a
loadable skill): [mission-template/](mission-template/).

## Session flow

```mermaid
flowchart LR
  Q[Request] --> IDX{ae-corpus}
  IDX -->|project mission| M[mission-project]
  IDX -->|generic| G[ae-dev-gates]
  M --> G
  G --> P[dbt plugin]
  G --> Tool[tool-* when relevant]
  M --> Task{L4 task?}
  Task -->|yes| L4[task file]
  Task -->|no| Impl[Mission deltas]
  L4 --> Impl
  Impl --> Out[Lint cost build MR]
```

## Package scope (shipped vs planned)

```mermaid
mindmap
  root((AE Corpus portable))
    Shipped
      ae-corpus
      ae-dev-gates
      Official dbt plugin external
    L0 stubs
      ae-data-modeling
      ae-documentation
      ae-data-testing
    L1 stubs
      tool-bigquery
      tool-data-studio
    Planned L1
      tool-omni
      tool-power-bi
      tool-dataform
      tool-sqlmesh
    Outside package
      mission-*
      project-*.md
      L4 tasks
      Ingestion
```
