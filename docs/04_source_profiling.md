## Initial Profiling Results

The profiling notebook successfully loaded all nine Olist source datasets and generated:

- Table-Level Statistics
- column-Level Metadata
- Row Counts
- Column Counts
- Data Types
- Null Counts
- Distinct-Value Counts

The results are persisted as Delta tables:

- profile_table_summary
- profile_column_summary
- profile_null_summary
- profile_duplicate_summary
- profile_key_quality_summary
- profile_run_history

## Null Analysis

The profiling framework generated column-level null statistics for every source dataset.

Metrics collected:

- Null Count
- Null Percentage
- Non-Null Count
- Non-Null Percentage

## Duplicate Analysis

The framework evaluates two duplicate categories:

1. Exact duplicate rows
2. Duplicate expected business keys

Results are stored in:
- `profile_duplicate_summary`

Business keys were defined according to the expected grain of each source dataset.

The geolocation dataset was not treated as unique at ZIP-prefix level because multiple coordinate records can exist for the same prefix.

![Duplicate analysis](../screenshots/04-source-profiling/04-duplicate-analysis.png)

## Business-Key Completeness

Expected business-key columns were tested for null and blank values.

Results are stored in:

- `profile_key_quality_summary`

![Key quality analysis](../screenshots/04-source-profiling/05-key-quality-analysis.png)

## Profiling Run History

Each profiling execution receives a unique run identifier and records:

- start timestamp;
- completion timestamp;
- duration;
- number of datasets;
- number of tables;
- number of columns;
- execution status.

Run metadata is stored in:

- `profile_run_history`

![Profiling run history](../screenshots/04-source-profiling/06-profile-run-history.png)