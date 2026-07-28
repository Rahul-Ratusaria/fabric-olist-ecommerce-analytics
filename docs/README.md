# Project Documentation

This folder contains the detailed technical and business documentation for the Microsoft Fabric Olist analytics project.

The documents are numbered in the order in which the project is implemented.

---

## Documentation Index

| Document | Description | Status |
|---|---|---|
| `01_project_charter.md` | Business problem, objectives, stakeholders and success criteria | Completed |
| `02_fabric_setup.md` | Fabric trial, workspace, Lakehouse and OneLake setup | Completed |
| `03_data_ingestion.md` | Kaggle-to-OneLake ingestion and validation | Completed |
| `04_source_profiling.md` | Schema, null, duplicate and source-quality analysis | Completed |
| `05_bronze_layer.md` | Raw Delta-table implementation and ingestion audit | Planned |
| `06_silver_layer.md` | Cleaning, standardization and enrichment rules | Planned |
| `07_data_quality.md` | Automated tests, quarantine and reconciliation | Planned |
| `08_gold_model.md` | Fact tables, dimensions, grains and features | Planned |
| `09_pipeline_orchestration.md` | Fabric Data Factory pipeline design | Planned |
| `10_semantic_model.md` | Relationships, DAX measures and model settings | Planned |
| `11_dashboard_design.md` | Dashboard pages, KPIs and visual specifications | Planned |
| `12_assumptions_limitations.md` | Known constraints and interpretation boundaries | Planned |
| `13_reproduction_guide.md` | Full project reproduction process | Planned |
| `14_future_enhancements.md` | Production-scale extensions | Planned |
| `glossary.md` | Business and technical terminology | Planned |

---

## Documentation Standards

Every technical document should contain:

1. Objective
2. Business or technical context
3. Implementation process
4. Code or configuration
5. Validation
6. Evidence
7. Design decisions
8. Security considerations
9. Result
10. Related repository files

---

## Naming Convention

Documentation files use two-digit numerical prefixes:

```text
01_
02_
03_
...
```

This keeps the project implementation sequence clear when viewed on GitHub.

---

## Screenshot References

Detailed documents may reference screenshots stored under:

```text
../screenshots/<phase-name>/
```

Example:

```markdown
![Source files in OneLake](../screenshots/03-data-ingestion/02-source-files-in-onelake.png)
```

Only the most important images should be placed in the main project README.

---

## Updating Documentation

After completing each phase:

1. create or update the relevant document;
2. add implementation evidence;
3. update its status in this README;
4. update the project-status table in the root README;
5. update any affected architecture diagram;
6. commit the documentation with the implementation files.