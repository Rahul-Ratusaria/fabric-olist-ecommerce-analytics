# Architecture

This folder contains the architecture diagrams for the **End-to-End Microsoft Fabric Olist E-Commerce Analytics** project. The diagrams document how the solution moves data from the Kaggle source through ingestion, profiling, Medallion Lakehouse processing, dimensional modelling, the Power BI semantic layer, and the final analytics report.

## End-to-End Architecture

![End-to-End Architecture](images/end_to_end_architecture.png)

The completed solution follows this high-level flow:

```text
Kaggle Olist E-Commerce Dataset
        ↓
Microsoft Fabric Data Pipeline
        ↓
OneLake Landing
        ↓
Source Profiling & Data Quality Checks
        ↓
Bronze Layer — Raw / Standardized Delta Tables
        ↓
Silver Layer — Validated / Cleaned Delta Tables + Quarantine
        ↓
Gold Layer — Dimensional Model + Audit / Reconciliation
        ↓
Power BI Semantic Model
        ↓
Power BI Analytics Report
```

The Fabric pipeline orchestrates the notebook sequence from landing through Gold, with downstream activities triggered only after successful completion of the preceding stage.

## Architecture Layers

| Layer / Component | Purpose                                                                           | Status   |
| ----------------- | --------------------------------------------------------------------------------- | -------- |
| External Source   | Olist E-Commerce CSV source files from Kaggle                                     | Complete |
| Landing           | Ingest source files into OneLake                                                  | Complete |
| Profiling         | Schema, null, duplicate, numeric, datetime, business-rule and integrity checks    | Complete |
| Bronze            | Standardized raw Delta tables with ingestion metadata and audit logging           | Complete |
| Silver            | Cleaned and validated entities with data-quality controls and quarantine handling | Complete |
| Gold              | Analytics-ready dimensional model, reconciliation and audit tables                | Complete |
| Semantic Model    | Relationships, DAX measures, KPIs and business semantics                          | Complete |
| Power BI Report   | Five-page interactive business analytics report                                   | Complete |
| GitHub            | Version-controlled notebooks, SQL, diagrams, documentation and report artifacts   | Complete |

## Medallion Architecture

The project implements a Medallion Lakehouse pattern in Microsoft Fabric.

### Bronze Layer

The Bronze layer preserves standardized source-level data in Delta format and captures ingestion metadata and load audit information. It provides the traceable foundation for downstream processing.

### Silver Layer

The Silver layer applies cleaning, validation, transformations and data-quality rules. Invalid records are separated through the quarantine framework with reason codes so that quality issues remain observable instead of being silently discarded.

### Gold Layer

The Gold layer provides the analytics-ready dimensional model consumed by the semantic model. It also contains audit, reconciliation and aggregate-validation outputs used to verify source-to-target processing.

## Profiling, Quality and Audit Framework

Data quality is treated as part of the architecture rather than as a reporting-only activity. The solution includes checks for:

- Schema consistency
- Null values
- Duplicate records
- Numeric validity
- Datetime validity
- Business rules
- Referential integrity
- Source-to-target reconciliation
- Load auditing
- Aggregate validation
- Quarantine monitoring

These controls are executed throughout the pipeline so that data is validated before it reaches the analytical model.

## Gold Dimensional Model

![Gold Star Schema](images/star_schema.png)

The completed Gold model contains **four dimensions and three fact tables**.

### Dimensions

- `dim_date`
- `dim_customer`
- `dim_product`
- `dim_seller`

### Facts

- `fact_order`
- `fact_order_item`
- `fact_payment`

The fact tables remain separate because they operate at different grains. Keeping order, order-item and payment facts independent avoids cross-grain multiplication and supports reliable aggregation in the semantic model.

The principal analytical relationships are:

```text
                    dim_date
                   /    |    \
                  /     |     \
         fact_order  fact_order_item  fact_payment
             ↑           ↑     ↑          ↑
      dim_customer  dim_product dim_seller dim_customer
```

The Power BI semantic model uses these Gold entities with one-to-many relationships and single-direction filtering where appropriate.

## Reporting Layer

The semantic model supports the final five-page Power BI report:

1. **Executive Overview**
2. **Sales & Revenue**
3. **Customer Intelligence**
4. **Operations & Logistics**
5. **Payments & Customer Experience**

The report uses reusable DAX measures and KPIs across revenue, orders, customers, products, sellers, delivery performance, payments, reviews and time intelligence.

## Folder Contents

```text
architecture/
│
├── images/
│   ├── end_to_end_architecture.png
│   └── star_schema.png
│
├── end_to_end_architecture.drawio
├── solution_architecture.drawio
├── star_schema.drawio
└── README.md
```

### Diagram Files

| File                                   | Description                                                                                                                           |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `end_to_end_architecture.drawio`     | Full project architecture covering source, orchestration, profiling, Medallion layers, quality controls, semantic model and reporting |
| `solution_architecture.drawio`       | Editable solution-level architecture diagram for the Microsoft Fabric implementation                                                  |
| `star_schema.drawio`                 | Editable Gold dimensional-model / semantic-model relationship diagram                                                                 |
| `images/end_to_end_architecture.png` | Rendered architecture image used in project documentation                                                                             |
| `images/star_schema.png`             | Rendered Gold model image used in project documentation                                                                               |

## Technology Mapping

| Architecture Area | Technology                                                     |
| ----------------- | -------------------------------------------------------------- |
| Source            | Kaggle Olist E-Commerce Dataset                                |
| Platform          | Microsoft Fabric                                               |
| Storage           | OneLake / Fabric Lakehouse                                     |
| Processing        | PySpark / Fabric Notebooks                                     |
| Table Format      | Delta Lake                                                     |
| Orchestration     | Fabric Data Pipeline                                           |
| Quality           | Profiling, validation, quarantine and reconciliation framework |
| Analytical Model  | Gold dimensional model                                         |
| Semantic Layer    | Power BI Semantic Model / DAX                                  |
| Visualization     | Power BI                                                       |
| Version Control   | Git / GitHub                                                   |

## Design Principles

The architecture is built around five principles:

1. **Layered processing** — ingestion, validation and analytics transformations remain logically separated.
2. **Data quality by design** — profiling, validation, quarantine and reconciliation are embedded in the pipeline.
3. **Grain-aware modelling** — order, item and payment facts remain separate to prevent incorrect aggregations.
4. **Reusable semantic logic** — business calculations are centralized as measures and KPIs in the semantic model.
5. **Traceability** — audit tables, run metadata and version-controlled project artifacts make the solution easier to understand and maintain.

---

This architecture represents the **completed project implementation**, not a future-state design.
