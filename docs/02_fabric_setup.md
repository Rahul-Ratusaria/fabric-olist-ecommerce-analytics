# Microsoft Fabric Environment Setup

## Objective

Establish the Microsoft Fabric development environment used by the Olist
e-commerce analytics project.

## Workspace

-   **Workspace:** `fabric-olist-dev`
-   **Capacity:** Microsoft Fabric Trial
-   **Purpose:** Development workspace for the Olist analytics solution

![Workspace](../screenshots/02-fabric-setup/workspace-created.png)

## Lakehouse

-   **Lakehouse:** `lh_olist_analytics`

The Lakehouse provides the OneLake-backed storage and managed
Delta-table environment used across ingestion, profiling, Bronze,
Silver, and Gold processing.

![Lakehouse](../screenshots/02-fabric-setup/lakehouse-created.png)

## Initial OneLake Folder Structure

``` text
Files/
├── landing/
│   └── olist/
│       └── source_csv/
├── reference/
└── logs/
```

![Lakehouse Folder
Structure](../screenshots/02-fabric-setup/lakehouse-folder-structure.png)

## Environment Role

The workspace contains the core Fabric components used by the project:

-   Lakehouse / OneLake storage;
-   Fabric notebooks;
-   managed Delta tables;
-   Fabric Data Pipeline orchestration;
-   semantic model;
-   Power BI report.

## Design Principle

The project keeps raw landing files, engineered Delta layers, analytical
modeling, orchestration, and reporting inside a single Fabric
development workspace while separating responsibilities logically by
processing layer.

## Result

The Fabric workspace and Lakehouse provide the shared environment for
the complete end-to-end analytics workflow.
