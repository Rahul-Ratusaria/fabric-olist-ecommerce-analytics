# Architecture Documentation

This folder contains the architecture diagrams and design decisions for the Microsoft Fabric Olist analytics project.

---

## Current Architecture

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
Lakehouse
    ├── Bronze
    ├── Silver
    └── Gold
          |
          v
Power BI Semantic Model
          |
          v
Power BI Dashboard
```

---

## Architecture Files

| File | Purpose | Status |
|---|---|---|
| `solution_architecture.drawio` | Overall solution and data-flow architecture | Created |
| `images/solution_architecture.png` | GitHub-friendly exported architecture image | To be exported |
| `medallion_architecture.drawio` | Detailed Bronze, Silver and Gold flow | Planned |
| `star_schema.drawio` | Gold-layer fact and dimension model | Planned |
| `images/star_schema.png` | Exported star-schema image | Planned |

---

## Architecture Decisions

### One Fabric Workspace

The project uses one development workspace:

```text
fabric-olist-dev
```

This keeps all Lakehouse, notebook, pipeline, semantic-model and report items in one manageable project container.

---

### One Lakehouse

The project uses one Lakehouse:

```text
lh_olist_analytics
```

Instead of creating separate Bronze, Silver and Gold Lakehouses, architectural separation is maintained through table-name prefixes:

```text
bronze_*
silver_*
dim_*
fact_*
```

This approach was chosen because:

- the dataset is appropriate for a single portfolio environment;
- it reduces cross-Lakehouse complexity;
- it is easier to reproduce using a free Fabric trial;
- it remains clear and explainable;
- it demonstrates the Medallion pattern without unnecessary infrastructure.

A production implementation could use separate Lakehouses, workspaces or schemas depending on governance and scale requirements.

---

### OneLake Landing Zone

The raw source files are stored under:

```text
Files/
└── landing/
    └── olist/
        └── source_csv/
```

The landing zone stores the extracted source CSV files before they are converted into Delta tables.

---

### Notebook-Based Kaggle Ingestion

The Kaggle dataset page is not used as a OneLake Shortcut because it is an authenticated web page rather than a supported storage path.

The project therefore uses a Fabric notebook and the Kaggle API to:

1. authenticate temporarily;
2. download the dataset;
3. extract the ZIP archive;
4. validate the expected files;
5. delete temporary credentials.

---

### Medallion Architecture

#### Bronze

The Bronze layer preserves source data with minimal modification.

Typical Bronze additions:

- source filename;
- batch identifier;
- ingestion timestamp;
- ingestion date.

#### Silver

The Silver layer performs:

- schema conversion;
- trimming and standardization;
- duplicate handling;
- null analysis;
- foreign-key validation;
- data-quality flags;
- derived operational features.

#### Gold

The Gold layer produces analytical tables such as:

```text
dim_date
dim_customer
dim_product
dim_seller
fact_order
fact_order_item
fact_payment
```

---

### Separate Fact-Table Grains

The project keeps order, item and payment analysis at separate grains.

This prevents incorrect aggregation caused by directly joining:

```text
multiple order items
        ×
multiple payment records
```

Order-level aggregates will be created before combining measures that require a common order grain.

---

### Semantic Model

The final semantic model will use a star-schema design and single-direction one-to-many relationships wherever possible.

Planned relationships include:

```text
dim_date      1 ─── * fact_order
dim_date      1 ─── * fact_order_item
dim_customer  1 ─── * fact_order
dim_product   1 ─── * fact_order_item
dim_seller    1 ─── * fact_order_item
```

---

## Diagram Maintenance

Whenever the solution changes:

1. update the `.drawio` source file;
2. export a PNG copy;
3. save the PNG inside `architecture/images/`;
4. update this README;
5. update the root README if the primary architecture changes;
6. commit both the source and exported image.

Suggested export size:

```text
Width: approximately 1600–2000 pixels
Background: white or transparent
Format: PNG
```

---

## Planned Diagram Development

### Phase 1

Basic end-to-end architecture.

### Phase 2

Detailed Medallion architecture showing:

- landing files;
- Bronze tables;
- Silver transformations;
- Gold facts and dimensions;
- audit and quarantine tables.

### Phase 3

Star-schema diagram showing table grains and relationships.

### Phase 4

Pipeline orchestration diagram showing:

- ingestion;
- profiling;
- Bronze load;
- Silver transformations;
- quality gate;
- Gold build;
- semantic-model refresh.