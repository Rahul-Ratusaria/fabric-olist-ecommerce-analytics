# Microsoft Fabric Pipeline

This folder documents the orchestration layer of the **Olist E-Commerce
Analytics** solution.

Microsoft Fabric Data Pipeline coordinates the complete engineering
workflow so that the notebooks execute in the correct dependency order
rather than being run manually.

## Pipeline Flow

``` text
NB - Landing
     ↓
NB - Profile Sources
     ↓
NB - Bronze
     ↓
NB - Silver
     ↓
NB - Gold
```

![Fabric Pipeline Execution Flow](pipeline_execution_flow.png)

## Pipeline Activities

| Order | Fabric Activity | Notebook | Responsibility |
| ------------ | ------------ | ------------ | ------------ |
| 1 | NB - Landing | `nb_00_ingest_olist.ipynb` | Ingest the Olist source CSV files into the OneLake landing zone |
| 2 | NB - Profile Sources | `nb_01_profile_sources.ipynb` | Profile source datasets and generate persistent data-quality outputs |
| 3 | NB - Bronze | `nb_02_load_bronze.ipynb` | Create standardized, source-faithful Bronze Delta tables and load audits |
| 4 | NB - Silver | `nb_03_build_silver.ipynb` | Clean, type, validate, enrich, quarantine, and reconcile source entities |
| 5 | NB - Gold | `nb_04_build_gold.ipynb` | Build dimensions, facts, surrogate keys, and Gold audit/reconciliation outputs |

## Dependency Strategy

Every activity is connected through an **On Success** dependency.

This means:

-   profiling starts only after landing succeeds;
-   Bronze starts only after profiling succeeds;
-   Silver starts only after Bronze succeeds;
-   Gold starts only after Silver succeeds.

A failed upstream stage therefore prevents dependent downstream
processing from continuing with incomplete data.

## Orchestration Benefits

The pipeline provides:

-   sequential execution;
-   dependency management;
-   centralized run monitoring;
-   execution history;
-   clear failure-point identification;
-   repeatable end-to-end processing;
-   a foundation for scheduling and additional production controls.

## Retry Configuration

The documented pipeline configuration uses:

-   **Retries:** 2
-   **Retry interval:** 30 seconds

## Final Status

| Component                     | Status     |
| ----------                    | ---------- |
| Landing activity              | Complete   |
| Source profiling activity     | Complete   |
| Bronze activity               | Complete   |
| Silver activity               | Complete   |
| Gold activity                 | Complete   |
| On Success dependencies       | Complete   |
| End-to-end pipeline execution | Complete   |

For detailed implementation context, see `pipeline_design.md` and
`../docs/08_pipeline.md`.
