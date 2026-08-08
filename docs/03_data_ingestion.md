# Data Ingestion

## Objective

Download the **Olist Brazilian E-Commerce** dataset from Kaggle and
store the extracted source CSV files in the Microsoft Fabric Lakehouse
landing zone.

## Source

-   **Dataset:** Olist Brazilian E-Commerce Public Dataset
-   **Provider:** Olist
-   **Platform:** Kaggle
-   **Dataset page:**
    `https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce`

## Source Files

The ingestion process validates the presence of nine CSV source files
covering:

-   customers;
-   sellers;
-   products;
-   orders;
-   order items;
-   payments;
-   reviews;
-   geolocation;
-   product-category translation.

## Target Location

``` text
lh_olist_analytics/
└── Files/
    └── landing/
        └── olist/
            └── source_csv/
```

## Ingestion Workflow

``` text
Kaggle API
    ↓
Fabric Notebook
    ↓
ZIP download in OneLake
    ↓
ZIP extraction
    ↓
Nine CSV files validated
    ↓
Temporary credential removed
```

## Ingestion Notebook

The ingestion logic is implemented in:

``` text
notebooks/nb_00_ingest_olist.ipynb
```

## Security Consideration

Credentials used for source access are treated as temporary runtime
inputs and are removed after the ingestion process. Credentials and
secrets must not be committed to GitHub or included in screenshots.

## Downstream Handoff

The landing files become the inputs for:

1.  source profiling;
2.  Bronze Delta-table creation.

No business transformation is performed in the landing step.

## Result

The source dataset is reproducibly landed in OneLake and validated
before downstream profiling and Medallion processing.
