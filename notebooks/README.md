# Microsoft Fabric Notebooks

This folder contains the five Microsoft Fabric notebooks that implement
the end-to-end data engineering workflow for the **Olist E-Commerce
Analytics** project.

The notebooks are executed sequentially by the Fabric Data Pipeline:

``` text
nb_00_ingest_olist
        ↓
nb_01_profile_sources
        ↓
nb_02_load_bronze
        ↓
nb_03_build_silver
        ↓
nb_04_build_gold
```

## Notebook Inventory

| Notebook |  Layer / Role |  Purpose | Status |
| ------------------------------- |  ----------------- |  ----------------- | ----------------- |
| `nb_00_ingest_olist.ipynb` | Landing | Download and land the Olist source CSV files in OneLake | Complete |
| `nb_01_profile_sources.ipynb` | Profiling / Data Quality | Profile source datasets and persist reusable quality metrics | Complete |
| `nb_02_load_bronze.ipynb` | Bronze | Create source-faithful Bronze Delta tables with lineage and audit metadata | Complete |
| `nb_03_build_silver.ipynb` | Silver | Clean, type, validate, enrich, quarantine, and reconcile source entities | Complete |
| `nb_04_build_gold.ipynb` | Gold | Build the dimensional model, facts, surrogate keys, and Gold audit controls | Complete |

## 1. `nb_00_ingest_olist.ipynb`

### Purpose

Ingest the public Olist Brazilian E-Commerce dataset from Kaggle into
the Fabric Lakehouse landing zone.

### Responsibilities

-   access the Kaggle source;
-   download the source archive;
-   extract the Olist CSV files;
-   validate the expected source-file set;
-   store the source files in OneLake;
-   remove temporary credential material after ingestion.

### Target

``` text
Files/
└── landing/
    └── olist/
        └── source_csv/
```

This notebook performs landing only. Business transformation is deferred
to downstream Medallion layers.

------------------------------------------------------------------------

## 2. `nb_01_profile_sources.ipynb`

### Purpose

Profile every landed source dataset before Bronze/Silver transformation
and create persistent data-quality evidence.

### Profiling Areas

-   table-level statistics;
-   column-level statistics;
-   null analysis;
-   duplicate analysis;
-   business-key completeness;
-   numeric profiling;
-   datetime profiling;
-   categorical profiling;
-   business-rule validation;
-   referential-integrity profiling;
-   dataset-health overview.

### Key Outputs

The notebook persists reusable `profile_*` Delta outputs covering source
quality and profiling run history. These outputs support auditability
and downstream quality assessment rather than relying only on notebook
display results.

------------------------------------------------------------------------

## 3. `nb_02_load_bronze.ipynb`

### Purpose

Load landed CSV files into standardized Bronze Delta tables while
preserving source fidelity.

### Design Principles

-   no business cleansing;
-   no deduplication;
-   preserve raw source values;
-   read source values safely before downstream typing;
-   add technical lineage and ingestion metadata;
-   reconcile source and target row counts.

### Processing

The notebook maps each source CSV to its corresponding `bronze_*` table,
adds ingestion metadata, writes managed Delta tables, and records
load/audit information.

### Outputs

``` text
9 bronze_* business tables
audit_bronze_load
audit_bronze_run_history
```

Bronze provides the traceable source-aligned foundation for Silver
processing.

------------------------------------------------------------------------

## 4. `nb_03_build_silver.ipynb`

### Purpose

Transform Bronze data into cleaned, validated, enriched, and
analysis-ready Silver entities.

### Core Transformations

The notebook processes:

-   customers;
-   orders;
-   order items;
-   products;
-   sellers;
-   payments;
-   reviews;
-   product-category translation;
-   geolocation.

### Processing Features

-   explicit schema conversion;
-   whitespace and blank normalization;
-   duplicate handling;
-   business-key validation;
-   business-rule validation;
-   quarantine of invalid records;
-   derived operational features;
-   product-category enrichment;
-   ZIP-level geolocation aggregation;
-   referential-integrity validation;
-   source-to-target reconciliation;
-   Silver audit logging.

### Quarantine Framework

Invalid records are captured in dedicated quarantine tables with quality
context instead of being silently discarded.

### Outputs

``` text
10 silver_* tables
9 quarantine tables
audit_silver_load
audit_silver_relationship
audit_silver_run_history
```

------------------------------------------------------------------------

## 5. `nb_04_build_gold.ipynb`

### Purpose

Build the final business-ready dimensional model from validated Silver
Delta tables.

### Dimensions

``` text
dim_date
dim_customer
dim_product
dim_seller
```

### Facts

``` text
fact_order
fact_order_item
fact_payment
```

### Fact Grains

  Fact                Grain
  ------------------- ----------------------------------------
  `fact_order`        One row per order
  `fact_order_item`   One row per order and item sequence
  `fact_payment`      One row per order and payment sequence

Order-item and payment facts remain separate to prevent cross-grain
record multiplication.

### Gold Features

-   deterministic surrogate keys;
-   explicit table grains;
-   fact-to-dimension key mapping;
-   customer, product, seller, and date dimensions;
-   independent order-level item aggregation;
-   independent order-level payment aggregation;
-   relationship validation;
-   financial reconciliation;
-   dimension-load audit logging;
-   fact-load audit logging;
-   run-level audit logging.

The resulting Gold tables provide the dimensional foundation for the
Power BI semantic model.

------------------------------------------------------------------------

## Orchestration

The notebooks are orchestrated through the Microsoft Fabric Data
Pipeline using sequential **On Success** dependencies.

``` text
Landing → Profiling → Bronze → Silver → Gold
```

This ensures a downstream stage runs only after its required upstream
stage has completed successfully.

------------------------------------------------------------------------

## Engineering Principles

The notebook implementation follows several consistent design
principles:

### Layer Separation

Each notebook has a distinct responsibility. Landing, profiling, raw
persistence, business transformation, and dimensional modeling are not
mixed into a single notebook.

### Data Quality Before Reporting

Quality checks are performed before curated analytical tables are
exposed to the reporting layer.

### Auditability

Bronze, Silver, and Gold processing records execution and reconciliation
information so that data movement can be validated.

### Quarantine Instead of Silent Loss

Invalid Silver records are separated with quality context rather than
being removed without traceability.

### Grain-Safe Modeling

Gold facts are maintained at distinct business grains to prevent
incorrect many-to-many aggregation behavior.

### Reusability

Helper functions and metadata-driven patterns are used where appropriate
to reduce repeated transformation logic.

------------------------------------------------------------------------

## Relationship to the Rest of the Repository

``` text
Source Data
    ↓
notebooks/nb_00_ingest_olist.ipynb
    ↓
notebooks/nb_01_profile_sources.ipynb
    ↓
notebooks/nb_02_load_bronze.ipynb
    ↓
notebooks/nb_03_build_silver.ipynb
    ↓
notebooks/nb_04_build_gold.ipynb
    ↓
Gold Dimensional Model
    ↓
Power BI Semantic Model
    ↓
Five-Page Power BI Dashboard
```

Related documentation is available under:

-   `docs/03_data_ingestion.md`
-   `docs/04_source_profiling.md`
-   `docs/05_bronze_layer.md`
-   `docs/06_silver_layer.md`
-   `docs/07_gold_layer.md`
-   `docs/08_pipeline.md`
-   `docs/09_semantic_model.md`
-   `architecture/`

------------------------------------------------------------------------

## Final Status

  Component                              Status
  -------------------------------------- ----------
  Landing ingestion notebook             Complete
  Source profiling notebook              Complete
  Bronze notebook                        Complete
  Silver notebook                        Complete
  Gold notebook                          Complete
  Data-quality controls                  Complete
  Quarantine framework                   Complete
  Audit / reconciliation controls        Complete
  Fabric pipeline integration            Complete
  Gold model handoff to semantic layer   Complete

The `notebooks/` folder therefore contains the complete executable
data-engineering path from external source ingestion through the curated
Gold dimensional model.
