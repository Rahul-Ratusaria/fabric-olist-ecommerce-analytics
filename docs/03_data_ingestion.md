# Data Ingestion

## Objective

Download the Olist Brazilian E-Commerce dataset directly from Kaggle and store the extracted CSV files inside the Microsoft Fabric Lakehouse landing zone.

## Source

- Dataset: Olist Brazalian E-Commerce Public Dataset
- Provider: OList
- Platform: Kaggle
- Dataset Link: https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce

## Target Location

```text
lh_olist_analytics/
└── Files/
    └── landing/
        └── olist/
            └── source_csv/
```

## Ingestion Workflow

```text
Kaggle API
    ↓
Fabric Notebook
    ↓
ZIP download in OneLake
    ↓
ZIP Extracted
    ↓
Nine CSV files validated
    ↓
Credential deleted
```

## Ingestion Notebook

Ingestion logic is implemented in `notebooks/nb_00_ingest_olist.ipynb`