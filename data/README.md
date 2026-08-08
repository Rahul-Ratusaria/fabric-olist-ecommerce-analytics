# Data

This folder documents the source data used by the **Microsoft Fabric Olist E-Commerce Analytics** project.

The project uses the public **Olist Brazilian E-Commerce dataset** as its external source. The raw CSV files are ingested into Microsoft Fabric and stored in OneLake as part of the project's automated ingestion and Medallion Lakehouse workflow.

The full raw dataset is intentionally **not duplicated in this GitHub repository**. This keeps the repository focused on the engineering implementation, analytics logic, documentation, and reproducible project structure.

---

## Source Dataset

**Dataset:** Brazilian E-Commerce Public Dataset by Olist
**Source platform:** Kaggle

**Domain:** [www.kaggle.com/datasets/olistbr/brazilian-ecommerce](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
**Domain:** E-commerce / Marketplace Analytics

The source contains customer, seller, product, order, payment, review, order-item, and geographic information for the Olist marketplace.

---

## Source Files

The project ingests **9 CSV files**.

| Source File                               | Description                                                                       | Main Use in Project                                      |
| ----------------------------------------- | --------------------------------------------------------------------------------- | -------------------------------------------------------- |
| `olist_customers_dataset.csv`           | Customer identifiers and customer geographic attributes                           | Customer dimension and geographic analysis               |
| `olist_geolocation_dataset.csv`         | ZIP-code prefixes with latitude, longitude, city, and state information           | Geographic reference and source profiling                |
| `olist_order_items_dataset.csv`         | Order-item transactions including product, seller, price, and freight information | Item-level sales, product, seller, and freight analytics |
| `olist_order_payments_dataset.csv`      | Payment type, installments, payment sequence, and payment value                   | Payment analytics and payment fact construction          |
| `olist_order_reviews_dataset.csv`       | Customer review scores and review-related information                             | Customer satisfaction and review analytics               |
| `olist_orders_dataset.csv`              | Order status and order lifecycle timestamps                                       | Core order fact, delivery, and operational analytics     |
| `olist_products_dataset.csv`            | Product identifiers, categories, and product attributes                           | Product dimension and category analytics                 |
| `olist_sellers_dataset.csv`             | Seller identifiers and seller geographic attributes                               | Seller dimension and seller performance analysis         |
| `product_category_name_translation.csv` | Portuguese-to-English product-category mapping                                    | Standardized English product-category reporting          |

---

## Data Flow

The source data follows the project's Microsoft Fabric processing architecture:

```text
Kaggle
   │
   ▼
9 Source CSV Files
   │
   ▼
Landing / OneLake
   │
   ▼
Source Profiling
   │
   ▼
Bronze Layer
Raw + Standardized Delta Tables
   │
   ▼
Silver Layer
Validated + Cleaned Delta Tables
   │
   ▼
Gold Layer
Dimensional Model
   │
   ▼
Direct Lake Semantic Model
   │
   ▼
Power BI Analytics Dashboard
```

The transformation and validation logic is implemented through the Fabric notebooks and orchestration pipeline maintained elsewhere in this repository.

---

## Data Profiling

Before downstream transformation, the source datasets pass through a dedicated profiling framework.

Profiling includes:

- schema inspection;
- row and column profiling;
- null analysis;
- duplicate checks;
- numeric validation;
- datetime validation;
- business-rule checks;
- referential-integrity checks;
- dataset health assessment.

Profiling outputs are persisted as dedicated `profile_*` Delta tables in Microsoft Fabric rather than as static files in this GitHub folder.

---

## Medallion Architecture

### Bronze

The Bronze layer preserves standardized versions of the ingested source datasets and maintains ingestion/audit metadata.

```text
9 bronze_* business tables
2 Bronze audit tables
```

### Silver

The Silver layer performs validation, cleaning, standardization, and quality enforcement.

```text
10 silver_* tables
9 quarantine tables
3 Silver audit tables
```

Invalid records are captured through the project's quarantine framework with reason codes rather than being silently discarded.

### Gold

The Gold layer provides the dimensional model used by the reporting layer.

#### Dimensions

```text
dim_date
dim_customer
dim_product
dim_seller
```

#### Facts

```text
fact_order
fact_order_item
fact_payment
```

The Gold layer also maintains audit, reconciliation, and aggregate-validation outputs.

---

## Analytical Grain

The final model deliberately separates different business grains.

| Table               | Grain                           |
| ------------------- | ------------------------------- |
| `fact_order`      | One row per order               |
| `fact_order_item` | One row per order item          |
| `fact_payment`    | One row per payment transaction |
| `dim_customer`    | One row per modeled customer    |
| `dim_product`     | One row per modeled product     |
| `dim_seller`      | One row per modeled seller      |
| `dim_date`        | One row per calendar date       |

Keeping the order, item, and payment facts separate avoids many-to-many analytical issues and prevents measures from being inflated by cross-grain joins.

---

## Why Raw CSV Files Are Not Stored Here

The repository does not need to duplicate the complete external dataset because the project is designed to demonstrate an **end-to-end Microsoft Fabric analytics implementation**, not to redistribute the source dataset.

The source files are loaded into the Fabric environment by the ingestion workflow and subsequently managed through OneLake and Delta tables.

This approach keeps GitHub focused on:

- Fabric notebooks;
- SQL and transformation logic;
- pipeline/orchestration design;
- architecture diagrams;
- semantic-model documentation;
- Power BI artifacts;
- data-quality implementation;
- project documentation.



---

## Data Governance Notes

- Raw source data is preserved before transformation.
- Data-quality validation occurs before curated analytical outputs are produced.
- Invalid records are quarantined with traceable reasons.
- Source-to-target reconciliation is maintained through audit and validation processes.
- Gold facts retain distinct analytical grains.
- Business-facing reporting consumes curated Gold-layer data through the semantic model.

---

## Related Repository Components

For implementation details, refer to the corresponding repository folders for:

- `architecture/` — end-to-end architecture and dimensional-model diagrams;
- notebook folders — ingestion, profiling, Bronze, Silver, and Gold processing;
- pipeline/orchestration artifacts — end-to-end Fabric workflow;
- `dashboard/` — final Power BI report and dashboard specification;
- `screenshots/` — evidence of the implemented Fabric solution and final dashboard.

---

## Status

| Component                          | Status      |
| ---------------------------------- | ----------- |
| Source dataset identified          | ✅ Complete |
| 9 source CSVs defined              | ✅ Complete |
| Fabric ingestion                   | ✅ Complete |
| Source profiling                   | ✅ Complete |
| Bronze processing                  | ✅ Complete |
| Silver validation & transformation | ✅ Complete |
| Quarantine handling                | ✅ Complete |
| Gold dimensional model             | ✅ Complete |
| Semantic model                     | ✅ Complete |
| Power BI reporting                 | ✅ Complete |

This folder therefore serves as the **data-source and data-flow documentation layer** of the repository rather than as storage for the complete raw Olist dataset.
