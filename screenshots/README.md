# Project Screenshots

This folder contains the visual evidence for the completed **Microsoft
Fabric Olist E-Commerce Analytics** project.

The screenshots make the implementation reviewable outside the original
Fabric workspace and preserve evidence of the solution even when the
development/trial environment is no longer available.

Screenshots are documentation artifacts only; they are **not inputs to
the data pipeline**.

------------------------------------------------------------------------

## Screenshot Inventory

``` text
screenshots/
├── 02-fabric-setup/
│   ├── lakehouse-created.png
│   ├── lakehouse-folder-structure.png
│   ├── sql-analytics-endpoint.png
│   └── workspace-created.png
│
├── 03-data-ingestion/
│   └── source-files-in-onelake.png
│
├── 04-source-profiling/
│   ├── 01-table-summary.png
│   ├── 02-column-summary.png
│   ├── 03-null-analysis.png
│   ├── 04-duplicate-analysis.png
│   ├── 05-key-quality-analysis.png
│   ├── 06-profile-run-history.png
│   ├── 07-numeric-profile.png
│   ├── 08-date-profile.png
│   ├── 09-categorical-profile.png
│   ├── 10-business-rule-profile.png
│   ├── 11-relationship-profile.png
│   └── 12-profile-overview.png
│
├── 05-bronze-layer/
│   ├── 01-bronze-tables.png
│   ├── 02-bronze-load-audit.png
│   ├── 03-bronze-schema.png
│   └── 04-bronze-metadata.png
│
├── 06-silver-layer/
│   ├── 01-core-silver-tables.png
│   ├── 02-silver-orders-schema.png
│   ├── 03-order-derived-features.png
│   ├── 04-core-quarantine-summary.png
│   ├── 05-core-silver-audit.png
│   ├── 06-all-silver-tables.png
│   ├── 07-seller-payment-review-samples.png
│   ├── 08-product-category-enrichment.png
│   ├── 09-geolocation-zip-lookup.png
│   ├── 10-silver-relationship-audit.png
│   ├── 11-complete-silver-audit.png
│   └── 12-silver-run-history.png
│
├── 07-gold-layer/
│   ├── 01-gold-dimensions.png
│   ├── 02-date-dimension.png
│   ├── 03-customer-dimension.png
│   ├── 04-product-dimension.png
│   ├── 05-seller-dimension.png
│   ├── 06-dimension-audit.png
│   ├── 07-gold-facts.png
│   ├── 08-fact-order.png
│   ├── 09-fact-order-item.png
│   ├── 10-fact-payment.png
│   ├── 11-fact-audit.png
│   ├── 12-gold-relationship-audit.png
│   └── 13-financial-reconciliation.png
│
├── 08-pipeline/
│   ├── 01-pipeline-design.png
│   ├── 02-notebook-properties.png
│   └── 03-dependency-view.png
│
├── 09-semantic-model/
│   ├── 01-semantic-model-tables.png
│   ├── 02-model-relationships.png
│   ├── 03-measures-table.png
│   ├── 04-measure-properties.png
│   ├── 05-complete-measure-library.png
│   └── 06-time-intelligence-validation.png
│
└── 10-dashboard/
    ├── 01 Executive Overview.png
    ├── 02 Sales & Revenue.png
    ├── 03 Customer Intelligence.png
    ├── 04 Operations & Logistics.png
    └── 05 Payments & Customer Experience.png
```

------------------------------------------------------------------------

## 02 --- Fabric Setup

Evidence of the Fabric development environment and Lakehouse foundation.

The screenshots demonstrate:

-   Fabric workspace creation;
-   Lakehouse creation;
-   OneLake folder structure;
-   SQL analytics endpoint availability.

These images support the environment setup documented in
`docs/02_fabric_setup.md`.

------------------------------------------------------------------------

## 03 --- Data Ingestion

Evidence that the Olist source files were successfully landed in
OneLake.

The screenshot demonstrates the source-file landing result used by the
downstream profiling and Medallion workflow.

Related documentation:

``` text
docs/03_data_ingestion.md
```

------------------------------------------------------------------------

## 04 --- Source Profiling

This folder contains the most detailed evidence for the project's
pre-transformation data-quality framework.

The screenshots cover:

-   table summary;
-   column summary;
-   null analysis;
-   duplicate analysis;
-   business-key quality;
-   profiling run history;
-   numeric profiling;
-   datetime profiling;
-   categorical profiling;
-   business-rule profiling;
-   relationship / referential-integrity profiling;
-   consolidated profile overview.

Related documentation:

``` text
docs/04_source_profiling.md
```

------------------------------------------------------------------------

## 05 --- Bronze Layer

Evidence for source-faithful Bronze Delta processing.

The screenshots cover:

-   Bronze table creation;
-   load-audit results;
-   Bronze schema;
-   technical ingestion and lineage metadata.

Related documentation:

``` text
docs/05_bronze_layer.md
```

------------------------------------------------------------------------

## 06 --- Silver Layer

Evidence for the project's cleaning, validation, enrichment, quarantine,
and reconciliation layer.

The screenshots cover:

-   core Silver tables;
-   typed order schema;
-   derived order features;
-   quarantine summaries;
-   Silver audit outputs;
-   complete Silver table inventory;
-   seller, payment, and review samples;
-   product-category enrichment;
-   ZIP-level geolocation lookup;
-   relationship audits;
-   complete Silver audit results;
-   run history.

Related documentation:

``` text
docs/06_silver_layer.md
```

------------------------------------------------------------------------

## 07 --- Gold Layer

Evidence for the final dimensional model.

The screenshots cover:

### Dimensions

-   `dim_date`
-   `dim_customer`
-   `dim_product`
-   `dim_seller`

### Facts

-   `fact_order`
-   `fact_order_item`
-   `fact_payment`

Additional evidence covers:

-   dimension audits;
-   fact audits;
-   Gold relationship validation;
-   financial reconciliation.

Related documentation:

``` text
docs/07_gold_layer.md
```

------------------------------------------------------------------------

## 08 --- Pipeline

Evidence for Microsoft Fabric orchestration.

The screenshots demonstrate:

-   complete pipeline design;
-   notebook activity configuration;
-   dependency configuration.

The implemented execution flow is:

``` text
Landing
   ↓
Profile Sources
   ↓
Bronze
   ↓
Silver
   ↓
Gold
```

Related documentation:

``` text
pipelines/
docs/08_pipeline.md
```

------------------------------------------------------------------------

## 09 --- Semantic Model

Evidence for the reporting semantic layer.

The screenshots cover:

-   semantic-model tables;
-   dimensional relationships;
-   centralized `_Measures` table;
-   measure properties and formatting;
-   complete measure library;
-   time-intelligence validation.

Related documentation:

``` text
docs/09_semantic_model.md
```

------------------------------------------------------------------------

## 10 --- Dashboard

This folder contains the five completed Power BI report pages.

### Page 1 --- Executive Overview

![Executive Overview](10-dashboard/01%20Executive%20Overview.png)

Provides a consolidated view of GMV, orders, customers, order value,
delivery performance, product categories, geography, and payment mix.

### Page 2 --- Sales & Revenue

![Sales & Revenue](10-dashboard/02%20Sales%20%26%20Revenue.png)

Analyzes monthly revenue, state performance, product categories,
sellers, product-level metrics, and category revenue concentration.

### Page 3 --- Customer Intelligence

![Customer Intelligence](10-dashboard/03%20Customer%20Intelligence.png)

Analyzes active, repeat, and new customers together with order
frequency, customer value, geography, and customer growth.

### Page 4 --- Operations & Logistics

![Operations &
Logistics](10-dashboard/04%20Operations%20%26%20Logistics.png)

Analyzes delivery rates, on-time performance, delays, delivery time,
freight behavior, state-level performance, and delivery outcomes.

### Page 5 --- Payments & Reviews

![Payments &
Reviews](10-dashboard/05%20Payments%20%26%20Customer%20Experience.png)

Analyzes payment methods, transaction behavior, installments,
review-score distribution, customer satisfaction, and satisfaction
trends.

Related documentation:

``` text
dashboard/README.md
docs/10_dashboard.md
```

------------------------------------------------------------------------

## Naming Convention

Implementation screenshots use a numeric prefix where multiple
screenshots exist within the same stage.

Examples:

``` text
01-table-summary.png
02-column-summary.png
03-null-analysis.png
```

The prefix keeps screenshots in the intended review order.

The dashboard screenshots retain descriptive page names so that each
image maps directly to its corresponding Power BI report page.

------------------------------------------------------------------------

## Security Rules

Before committing screenshots, verify that they do not expose:

-   email addresses;
-   passwords;
-   Kaggle credentials;
-   API keys;
-   access tokens;
-   tenant-sensitive identifiers;
-   browser cookies;
-   signed URLs;
-   private account information;
-   confidential browser tabs or bookmarks.

Crop unnecessary browser or desktop areas where practical.

------------------------------------------------------------------------

## Documentation Usage

The screenshot library is intentionally separated from the main project
documentation.

High-value screenshots can be embedded in the repository's root README,
while detailed implementation evidence should be referenced from the
corresponding documents under `docs/`.

This keeps the main README concise while still allowing technical
reviewers to inspect the full implementation.

------------------------------------------------------------------------

## Coverage Summary

| Project Stage           | Screenshot Folder        | Evidence                                           |
| ----------------------- | ------------------------ | -----------------------                            |
| Fabric Setup            | `02-fabric-setup/`       | Workspace, Lakehouse, folders, SQL endpoint        |
| Data Ingestion          | `03-data-ingestion/`     | Source files landed in OneLake                     |
| Source Profiling        | `04-source-profiling/`   | Profiling and quality framework                    |
| Bronze                  | `05-bronze-layer/`       | Tables, schema, metadata, load audit               |
| Silver                  | `06-silver-layer/`       | Clean tables, quarantine, enrichment, audits       |
| Gold                    | `07-gold-layer/`         | Dimensions, facts, audits, reconciliation          |
| Pipeline                | `08-pipeline/`           | Orchestration and dependencies                     |
| Semantic Model          | `09-semantic-model/`     | Tables, relationships, measures, time intelligence |
| Dashboard               | `10-dashboard/`          | Five completed Power BI pages                      |

## Final Status

The screenshot library now provides visual evidence across the complete
implementation path:

**Fabric Setup → Ingestion → Profiling → Bronze → Silver → Gold →
Pipeline → Semantic Model → Power BI Dashboard**

**Status: Complete**
