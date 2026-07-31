# Olist E-Commerce Analytics Platform using Microsoft Fabric

An end-to-end Microsoft Fabric Data Engineering and Analytics project implementing a modern Medallion Architecture (Landing → Bronze → Silver → Gold) on the Brazilian Olist E-Commerce dataset.

This project demonstrates production-style data engineering practices including ingestion, Delta Lake, data quality validation, quarantine handling, audit logging, dimensional modeling, semantic modeling, Power BI dashboarding, CI/CD readiness, and GitHub documentation.

---

# Project Overview

The objective of this project is to build a complete analytics platform using Microsoft Fabric while following enterprise data engineering best practices.

The pipeline begins with raw CSV files stored in OneLake and progresses through multiple Medallion layers until business-ready analytical dashboards are produced.

---

# Tech Stack

- Microsoft Fabric
- OneLake
- Lakehouse
- Apache Spark
- PySpark
- Delta Lake
- SQL Endpoint
- Power BI
- Git
- GitHub
- VS Code

---

# Architecture

```
Source CSV Files
        │
        ▼
Landing (OneLake Files)
        │
        ▼
Bronze Layer
Raw Delta Tables
        │
        ▼
Silver Layer
Validated Business Tables
        │
        ▼
Gold Layer
Star Schema
        │
        ▼
Power BI Dashboard
```

---

# Repository Structure

```
fabric-olist-analytics/
│
├── architecture/
├── dashboards/
├── datasets/
├── docs/
├── notebooks/
├── screenshots/
├── sql/
├── .gitignore
├── LICENSE
└── README.md
```

---

# Current Progress

| Phase | Status |
|---------|---------|
| Project Planning | ✅ Completed |
| Repository Setup | ✅ Completed |
| Architecture Design | ✅ Completed |
| Landing Layer | ✅ Completed |
| Source Profiling | ✅ Completed |
| Bronze Layer | ✅ Completed |
| Silver Layer | ✅ Completed |
| Gold Layer | ✅ Completed |
| Semantic Model | ⏳ Upcoming |
| Power BI Dashboard | ⏳ Upcoming |
| CI/CD | ⏳ Upcoming |

---

# Landing Layer

The Landing layer stores the original Olist CSV files inside Microsoft OneLake.

Characteristics

- Immutable source files
- No transformations
- Raw historical data
- Source of truth

---

# Bronze Layer

The Bronze layer converts raw CSV files into managed Delta tables.

Implemented Features

- Dynamic ingestion framework
- Metadata-driven loading
- Delta Lake storage
- SHA-256 record hashing
- Technical lineage
- Audit logging
- Source-to-target reconciliation

Generated Tables

- bronze_customers
- bronze_orders
- bronze_order_items
- bronze_products
- bronze_sellers
- bronze_order_reviews
- bronze_order_payments
- bronze_geolocation
- bronze_category_translation

Audit Tables

- audit_bronze_load
- audit_bronze_run_history

Screenshot

![Bronze](screenshots/05-bronze-layer/01-bronze-tables.png)

Documentation

docs/05_bronze_layer.md

---

# Silver Layer

The Silver layer transforms raw Bronze tables into clean business entities.

Implemented Features

- Explicit data type conversion
- Data standardization
- Null handling
- Whitespace removal
- Business rule validation
- Data quality flags
- Quarantine framework
- Duplicate removal
- Feature engineering
- Product category translation
- Geolocation aggregation
- Referential integrity validation
- Audit logging

Silver Tables

- silver_customers
- silver_orders
- silver_order_items
- silver_products
- silver_sellers
- silver_order_payments
- silver_order_reviews
- silver_category_translation
- silver_geolocation
- silver_geolocation_zip

Audit Tables

- audit_silver_load
- audit_silver_relationship
- audit_silver_run_history

Screenshot

![Silver](screenshots/06-silver-layer/06-all-silver-tables.png)

Documentation

docs/06_silver_layer.md

---

## Gold Dimensional Model

The Gold layer reorganizes the validated Silver entities into a business-ready star schema.

### Dimensions

- `dim_date`
- `dim_customer`
- `dim_product`
- `dim_seller`

### Facts

- `fact_order`
- `fact_order_item`
- `fact_payment`

Each fact retains an explicit business grain. Order items and payments remain separate to prevent cross-grain value multiplication.

The framework validates:

- natural and surrogate-key uniqueness;
- fact-table grains;
- fact-to-dimension relationships;
- Silver-to-Gold row counts;
- GMV, freight and payment reconciliation.

![Gold star schema](architecture/images/star_schema.png)

![Gold facts](screenshots/07-gold-layer/07-gold-facts.png)

Detailed implementation: [Gold Layer Documentation](docs/07_gold_layer.md)

# Upcoming Work

Planned deliverables include

- Incremental Loading
- SQL Analytics Endpoint
- Semantic Model
- Power BI Dashboard
- Deployment Pipeline

---

# Documentation

| Document | Description |
|------------|----------------|
| docs/project_charter.md | Project objectives |
| docs/05_bronze_layer.md | Bronze implementation |
| docs/06_silver_layer.md | Silver implementation |
| docs/07_gold_layer.md | Gold implementation |

---

# Dataset

Olist Brazilian E-Commerce Dataset

https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce

---

# Author

Rahul Ratusaria

Senior Data Analyst

Microsoft Fabric | PySpark | SQL | Power BI | Data Engineering