# Microsoft Fabric Notebooks

This folder stores exported Microsoft Fabric notebooks used for ingestion, profiling, transformation, data quality and Gold-layer modelling.

---

## Notebook Execution Order

| Sequence | Fabric notebook | Local export | Purpose | Status |
|---:|---|---|---|---|
| 1 | `nb_00_ingest_olist` | `nb_00_ingest_olist.ipynb` | Download and validate the Olist dataset | Completed |
| 2 | `nb_01_profile_sources` | `nb_01_profile_sources.ipynb` | Profile raw source files and identify data-quality issues | Completed |
| 3 | `nb_02_load_bronze` | `nb_02_load_bronze.ipynb` | Load raw CSV data into Bronze Delta tables | Completed |
| 4 | `nb_03_transform_silver_core` | `nb_03_transform_silver_core.ipynb` | Transform orders, items, customers and products | Planned |
| 5 | `nb_04_transform_silver_supporting` | `nb_04_transform_silver_supporting.ipynb` | Transform sellers, payments, reviews and geolocation | Planned |
| 6 | `nb_05_data_quality` | `nb_05_data_quality.ipynb` | Execute automated data-quality and reconciliation tests | Planned |
| 7 | `nb_06_build_gold` | `nb_06_build_gold.ipynb` | Build dimensions, facts and analytical features | Planned |

---

## Notebook Design Standards

Every notebook should contain:

### 1. Markdown Header

- notebook purpose;
- source tables or files;
- target tables;
- expected outputs;
- security considerations.

### 2. Configuration Section

Paths and project parameters should be defined near the beginning.

Example:

```python
LAKEHOUSE_ROOT = "/lakehouse/default"
RUN_DATE = "YYYY-MM-DD"
BATCH_ID = "<generated-value>"
```

### 3. Import Section

All imports should be grouped in one clearly labelled cell.

### 4. Validation

Notebooks should fail clearly when:

- required source files are missing;
- expected columns are unavailable;
- critical data-quality tests fail;
- output tables cannot be created.

### 5. Audit Output

Where applicable, notebooks should write:

- batch identifier;
- source and target row counts;
- execution timestamp;
- status;
- failed-test count.

### 6. Clean Output

Large data previews and unnecessary cell outputs should be cleared before committing to GitHub.

---

## Security Rules

Never include:

- `kaggle.json`;
- API keys;
- Fabric access tokens;
- signed URLs;
- personal email addresses;
- credential contents;
- company-sensitive data.

Credentials must be excluded through `.gitignore` and removed from OneLake after their intended use.

---

## Notebook Export Process

After updating a notebook in Fabric:

1. save the Fabric notebook;
2. download or export it as `.ipynb`;
3. replace the corresponding file in this folder;
4. inspect the local file for sensitive output;
5. clear unnecessary output if required;
6. commit the updated notebook.

---

## Current Notebook

### `nb_00_ingest_olist.ipynb`

The ingestion notebook:

- installs or uses the Kaggle client;
- configures the credential temporarily;
- downloads the Olist dataset;
- extracts the ZIP archive;
- verifies the expected nine source files;
- generates a source inventory;
- deletes temporary credentials.


### `nb_01_profile_sources.ipynb`

Status: **In Progress**

The profiling notebook currently generates:

- table-level row and column counts;
- column data types and cardinality;
- null and non-null statistics;
- exact-row duplicate counts;
- business-key duplicate analysis;
- business-key completeness checks;
- profiling execution metadata.

Generated Delta tables:

- `profile_table_summary`
- `profile_column_summary`
- `profile_null_summary`
- `profile_duplicate_summary`
- `profile_key_quality_summary`
- `profile_run_history`
- `profile_numeric_summary`
- `profile_datetime_summary`
- `profile_categorical_summary`
- `profile_business_rule_summary`
- `profile_relationship_summary`

The notebook also validates source referential integrity across:

- orders and customers;
- order items and orders;
- order items and products;
- order items and sellers;
- payments and orders;
- reviews and orders.


## `nb_02_load_bronze.ipynb`

The bronze notebook:

- dynamically loads all nine source CSV files;
- preserves all source fields as strings;
- adds technical lineage metadata;
- generates deterministic SHA-256 row hashes;
- writes managed Delta tables;
- reconciles source and target row counts;
- stores table-level and run-level audit history.

Generated tables:

- nine `bronze_*` tables;
- `audit_bronze_load`;
- `audit_bronze_run_history`