# Enterprise E-Commerce Analytics Platform using Microsoft Fabric

An end-to-end data engineering and business intelligence portfolio project built using Microsoft Fabric, OneLake, Lakehouse, PySpark, SQL, Data Factory and Power BI.

The project uses the public Brazilian E-Commerce Dataset by Olist and demonstrates how multiple relational CSV files can be ingested, validated, transformed, modelled and presented through an interactive business dashboard.

---

## Project Status

| Phase | Status |
|---|---|
| GitHub repository setup | Completed |
| Project charter | Completed |
| Solution architecture | Completed |
| Microsoft Fabric workspace | Completed |
| Lakehouse and OneLake setup | Completed |
| Kaggle-to-OneLake ingestion | Completed |
| Source-data validation | Completed |
| Source profiling | Completed |
| Bronze layer | Not started |
| Silver layer | Not started |
| Data-quality framework | Not started |
| Gold dimensional model | Not started |
| Pipeline orchestration | Not started |
| Power BI semantic model | Not started |
| Power BI dashboard | Not started |
| Final documentation and demo | Not started |

The status table will be updated as the project progresses.

---

## Business Problem

The source data is distributed across multiple CSV files containing orders, customers, products, sellers, payments, reviews, order items and geolocation information.

Without a centralized analytics platform, business users cannot easily:

- monitor overall marketplace performance;
- understand customer purchasing behaviour;
- analyse product-category performance;
- compare seller contribution;
- identify delivery delays;
- study payment behaviour;
- connect customer reviews with operational performance;
- verify whether analytical results are based on reliable data.

The objective of this project is to create a centralized Microsoft Fabric analytics platform that converts raw Olist data into business-ready insights.

---

## Business Objectives

The platform is designed to answer the following questions:

- How are GMV, order volume and average order value changing over time?
- Which product categories and sellers contribute the most value?
- Which customer states generate the highest demand?
- What percentage of eligible deliveries arrive late?
- How do delivery delays affect review scores?
- Which payment methods and instalment patterns are most common?
- What proportion of customers make repeat purchases?
- Which data-quality issues can affect dashboard reliability?

---

## Dataset

The project uses the:

**Brazilian E-Commerce Public Dataset by Olist**

Kaggle dataset identifier:

```text
olistbr/brazilian-ecommerce
```

The dataset contains approximately 100,000 marketplace orders and includes nine related CSV files.

### Source Files

| Source file | Main purpose |
|---|---|
| `olist_orders_dataset.csv` | Order status and lifecycle timestamps |
| `olist_order_items_dataset.csv` | Products, sellers, item prices and freight |
| `olist_customers_dataset.csv` | Customer identifiers and geography |
| `olist_products_dataset.csv` | Product attributes and categories |
| `olist_sellers_dataset.csv` | Seller information and geography |
| `olist_order_payments_dataset.csv` | Payment types, instalments and values |
| `olist_order_reviews_dataset.csv` | Review scores and comments |
| `olist_geolocation_dataset.csv` | ZIP-prefix geographical coordinates |
| `product_category_name_translation.csv` | Portuguese-to-English category translation |

The raw source files are not stored in this GitHub repository. They are acquired directly from Kaggle through a Microsoft Fabric notebook.

---

## Solution Architecture

```text
Olist Dataset on Kaggle
          |
          v
Microsoft Fabric Notebook
          |
          v
OneLake Landing Zone
          |
          v
Bronze Delta Tables
          |
          v
Silver Cleaned and Validated Tables
          |
          v
Gold Fact and Dimension Tables
          |
          v
Power BI Semantic Model
          |
          v
Executive Analytics Dashboard
```

The architecture follows the Medallion design pattern:

- **Bronze:** raw source representation with ingestion metadata;
- **Silver:** cleaned, typed, standardized and validated records;
- **Gold:** business-ready fact tables, dimensions and analytical features.

Detailed architecture documentation is available in the [`architecture`](architecture/) folder.

---

## Microsoft Fabric Components

| Component | Purpose |
|---|---|
| Microsoft Fabric Workspace | Project-level cloud container |
| OneLake | Unified storage layer used by Fabric |
| Lakehouse | File and Delta-table storage |
| Fabric Notebook | Kaggle ingestion, profiling and PySpark transformations |
| Data Pipeline | Workflow orchestration and dependency management |
| SQL Analytics Endpoint | SQL validation and analytical querying |
| Power BI Semantic Model | Relationships, measures and business definitions |
| Power BI Report | Interactive analytical dashboard |
| GitHub | Version control, documentation and portfolio evidence |

---

## Current Fabric Environment

### Workspace

```text
fabric-olist-dev
```

### Lakehouse

```text
lh_olist_analytics
```

### OneLake Landing Structure

```text
Files/
├── landing/
│   └── olist/
│       └── source_csv/
├── reference/
└── logs/
```

The project uses one Lakehouse with table-name prefixes:

```text
bronze_*
silver_*
dim_*
fact_*
audit_*
quarantine_*
```

This design keeps the portfolio implementation manageable while preserving clear architectural separation.

---

## Data Ingestion

The dataset is downloaded directly from Kaggle through the Fabric notebook:

```text
nb_00_ingest_olist
```

The ingestion workflow is:

```text
Kaggle API
    |
    v
Fabric Notebook
    |
    v
ZIP downloaded into OneLake
    |
    v
CSV files extracted
    |
    v
Expected source inventory validated
    |
    v
Temporary credentials removed
```

The notebook validates that all nine expected CSV files are available before the ingestion phase is considered successful.

![Olist source files stored in OneLake](screenshots\03-data-ingestion\source-files-in-onelake.png)

Detailed implementation is available in:

[Data Ingestion Documentation](docs/03_data_ingestion.md)

---

## Security Controls

The project follows the following credential-handling practices:

- Kaggle credentials are never hard-coded into notebook code.
- `kaggle.json` is excluded through `.gitignore`.
- Credentials are used temporarily during ingestion.
- Temporary credential copies are deleted after successful ingestion.
- Notebook output never displays credential contents.
- No Fabric authentication token or signed URL is stored in GitHub.
- Only public and non-sensitive data is used.

This is a learning implementation. A production solution would normally use a managed secret store and stronger identity-based access controls.

---

## Planned Data Processing

### Bronze Layer

The Bronze layer will:

- preserve raw source column values;
- load data primarily as strings;
- add batch and ingestion metadata;
- create source-to-target audit records;
- maintain reproducibility.

### Silver Layer

The Silver layer will include:

- explicit schema enforcement;
- timestamp and numeric conversion;
- whitespace and text standardization;
- duplicate handling;
- null analysis;
- invalid-value flags;
- foreign-key validation;
- category translation;
- geolocation aggregation;
- derived delivery and order features.

### Gold Layer

The Gold layer will contain:

```text
dim_date
dim_customer
dim_product
dim_seller
fact_order
fact_order_item
fact_payment
```

The model will use separate facts at their correct business grains to prevent payment and order-item double counting.

---

## Planned Data-Quality Framework

The project will test:

- required-key completeness;
- business-key uniqueness;
- referential integrity;
- valid order status;
- review score range;
- non-negative prices and payments;
- timestamp sequence validity;
- delivered-order timestamp completeness;
- source-to-Silver reconciliation;
- Silver-to-Gold reconciliation;
- GMV and payment-value consistency.

Invalid records will be documented and, where appropriate, stored in quarantine tables rather than silently removed.

---

## Planned Dashboard Pages

The final Power BI report will contain five main pages.

### 1. Executive Overview

- Total GMV
- Orders
- Average order value
- Customers
- Late-delivery rate
- Average review score
- Monthly performance
- Top categories
- State-level demand
- Order-status distribution

### 2. Sales and Product Performance

- Category GMV
- Category contribution
- Product ranking
- Seller contribution
- Freight ratio
- Average item price
- Seller and category concentration

### 3. Customer and Payment Analysis

- Unique customers
- New and repeat customers
- Customer geography
- Orders per customer
- Payment-method mix
- Instalment behaviour
- Optional RFM segmentation

### 4. Logistics and Customer Experience

- Average and median delivery time
- Late-delivery rate
- Delay distribution
- Seller and state delay performance
- Review-score distribution
- Relationship between delivery delay and review score

### 5. Data Quality and Monitoring

- Latest pipeline run
- Ingestion row counts
- Passed and failed quality tests
- Critical failures
- Source-to-target reconciliation
- Null analysis
- Refresh status

---

## Important Metric Definitions

### Gross Merchandise Value

```text
GMV = Sum of order-item price
```

GMV is not treated as profit or accounting revenue because product cost, tax, commission and operating expenses are not available.

### Average Order Value

```text
Average Order Value = Total GMV / Distinct Orders
```

### Late Delivery Rate

```text
Late Delivery Rate =
Late eligible delivered orders /
Eligible delivered orders
```

Only orders with both actual and estimated delivery dates are included in the denominator.

### Freight Share

```text
Freight Share =
Total Freight /
(Total GMV + Total Freight)
```

A complete KPI dictionary will be maintained in the `docs` folder as the project progresses.

---

## Repository Structure

```text
fabric-olist-ecommerce-analytics/
├── README.md
├── LICENSE
├── .gitignore
├── architecture/
│   ├── README.md
│   ├── solution_architecture.drawio
│   └── images/
├── docs/
│   ├── README.md
│   ├── 01_project_charter.md
│   ├── 02_fabric_setup.md
│   └── 03_data_ingestion.md
├── notebooks/
│   ├── README.md
│   └── nb_00_ingest_olist.ipynb
├── pipelines/
│   └── README.md
├── powerbi/
│   └── README.md
├── screenshots/
│   ├── README.md
│   ├── fabric-setup/
│   └── 03-data-ingestion/
├── sql/
│   └── README.md
└── demo/
    └── README.md
```

The repository structure will expand as additional phases are completed.

---

## Documentation

| Document | Description |
|---|---|
| [Project Charter](docs/01_project_charter.md) | Business problem, objectives, stakeholders and success criteria |
| [Fabric Setup](docs/02_fabric_setup.md) | Workspace, Lakehouse and OneLake configuration |
| [Data Ingestion](docs/03_data_ingestion.md) | Kaggle acquisition, validation and credential handling |
| [Architecture](architecture/README.md) | Solution components and architecture decisions |

---

## Reproducing the Project

Current reproduction steps:

1. Create or activate a Microsoft Fabric trial.
2. Create the `fabric-olist-dev` workspace.
3. Create the `lh_olist_analytics` Lakehouse.
4. Create the OneLake landing folder structure.
5. Generate a Kaggle API credential.
6. Temporarily upload the credential to the Lakehouse.
7. Import and run `nb_00_ingest_olist`.
8. Validate that all nine source CSV files are available.
9. Delete temporary Kaggle credentials.

The reproduction guide will be expanded after each implementation phase.

---

## Assumptions and Limitations

- The dataset is historical and static.
- The project demonstrates batch ingestion rather than a live production feed.
- GMV is used as a marketplace-value metric and not as profit.
- Customer analysis depends on the distinction between `customer_id` and `customer_unique_id`.
- Geolocation is based on ZIP-prefix level coordinates.
- Some orders may contain incomplete lifecycle timestamps.
- The Fabric trial may expire, so GitHub stores code, documentation and visual evidence.
- Enterprise secret management, deployment pipelines and production SLAs are outside the current free implementation.

---

## Future Enhancements

Planned enhancements include:

- parameterized ingestion;
- incremental-load simulation;
- Delta `MERGE` operations;
- reusable data-quality functions;
- audit and control tables;
- customer RFM segmentation;
- delivery-distance analysis;
- seller concentration analysis;
- Fabric deployment pipelines;
- Git integration;
- automated semantic-model refresh;
- CI/CD validation;
- alerting and monitoring.

---

## Skills Demonstrated

- Microsoft Fabric
- OneLake
- Lakehouse
- Fabric Notebooks
- PySpark
- Delta Lake
- Data Factory pipelines
- SQL analytics
- Dimensional modelling
- Star schema
- Data-quality testing
- Power BI
- DAX
- Direct Lake
- Git
- GitHub documentation

---

## Licence

Project code and documentation are available under the licence included in this repository.

The Olist dataset remains subject to its original source terms and is not redistributed through this repository.