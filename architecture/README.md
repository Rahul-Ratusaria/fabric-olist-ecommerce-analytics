# Solution Architecture

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
| Gold | Planned |

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