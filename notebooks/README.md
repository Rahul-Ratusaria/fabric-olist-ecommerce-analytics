# Microsoft Fabric Notebooks

This folder contains all Microsoft Fabric notebooks used in the Medallion Architecture.

---

| Notebook | Purpose | Status |
|------------|------------------------------|-----------|
| nb_01_profile_sources.ipynb | Source profiling | Completed |
| nb_02_load_bronze.ipynb | Bronze ingestion | Completed |
| nb_03_build_silver.ipynb | Silver transformation | Completed |
| nb_04_build_gold.ipynb | Gold dimensional model | Completed |

---

## nb_01_profile_sources.ipynb

Performs automated profiling of all source datasets.

Features

- Row counts
- Column statistics
- Null profiling
- Duplicate analysis
- Business key validation
- Numeric statistics
- Categorical profiling

Outputs

- profile_table_summary
- profile_column_summary
- profile_null_summary
- profile_duplicate_summary
- profile_numeric_summary
- profile_categorical_summary
- profile_business_rule_summary
- profile_key_quality_summary
- profile_run_history

---

## nb_02_load_bronze.ipynb

Loads raw CSV files into Bronze Delta tables.

Features

- Dynamic ingestion
- SHA-256 hashing
- Technical lineage
- Metadata columns
- Audit framework
- Row-count reconciliation

Outputs

- 9 Bronze tables
- audit_bronze_load
- audit_bronze_run_history

---

## nb_03_build_silver.ipynb

Transforms Bronze Delta tables into standardized Silver tables.

Features

- Data type conversion
- Data cleansing
- Duplicate handling
- Business rule validation
- Quarantine framework
- Feature engineering
- Category translation
- ZIP-level aggregation
- Referential integrity validation
- Audit framework

Outputs

- 10 Silver tables
- 9 Quarantine tables
- audit_silver_load
- audit_silver_relationship
- audit_silver_run_history

---

### `nb_04_build_gold.ipynb`

Status: **Completed**

The Gold notebook creates four dimensions and three fact tables.

Dimensions:

- `dim_date`;
- `dim_customer`;
- `dim_product`;
- `dim_seller`.

Facts:

- `fact_order`;
- `fact_order_item`;
- `fact_payment`.

The notebook implements:

- deterministic surrogate keys;
- explicit fact-table grains;
- independent order-level aggregation;
- fact-to-dimension key mapping;
- relationship validation;
- financial reconciliation;
- dimension, fact and run-level audit logging.