# Solution Architecture

## End-to-End Architecture

The complete solution integrates source ingestion, automated profiling, Medallion Lakehouse processing, dimensional modelling, pipeline orchestration and business intelligence.

![End-to-end architecture](images/end_to_end_architecture.png)

### Data Flow

```text
Kaggle
    ↓
OneLake Landing
    ↓
Source Profiling
    ↓
Bronze Delta Tables
    ↓
Silver Validated Entities
    ↓
Gold Star Schema
    ↓
Power BI Semantic Model
    ↓
Executive Dashboard
```

This folder contains architecture diagrams used throughout the project.

Current diagrams include

- Overall Solution Architecture
- Medallion Architecture
- Data Flow
- Future CI/CD Architecture

---

## Current Medallion Status

| Layer | Status |
|----------|----------|
| Landing | Completed |
| Bronze | Completed |
| Silver | Completed |
| Gold | Completed |

---

## Architecture Components

- OneLake
- Lakehouse
- Spark Notebooks
- Delta Tables
- SQL Analytics Endpoint
- Power BI

## Gold Star Schema

The planned Gold model contains four dimensions and three fact tables.

![Gold star schema](images/star_schema.png)

The facts remain separate to prevent cross-grain multiplication between order items and payment records.