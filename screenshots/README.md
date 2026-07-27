# Project Screenshots

This folder contains visual evidence of the Microsoft Fabric implementation.

The screenshots are included because external viewers generally cannot access the private Fabric workspace, and the Fabric trial may expire after the project is completed.

---

## Purpose

Screenshots are used to demonstrate:

- workspace creation;
- Lakehouse configuration;
- OneLake folder structure;
- notebook execution;
- source-file validation;
- Bronze, Silver and Gold tables;
- data-quality results;
- pipeline orchestration;
- semantic model;
- Power BI dashboard.

Screenshots are documentation evidence and are not used by the data pipeline.

---

## Folder Structure

```text
screenshots/
├── fabric-setup/
├── 03-data-ingestion/
├── 04-source-profiling/
├── 05-bronze-layer/
├── 06-silver-layer/
├── 07-data-quality/
├── 08-gold-model/
├── 09-pipeline/
├── 10-semantic-model/
└── 11-dashboard/
```

Folders will be added as the project progresses.

---

## Naming Convention

Screenshot files should begin with a sequence number.

Example:

```text
01-workspace-created.png
02-lakehouse-created.png
03-folder-structure.png
```

This keeps screenshots in the correct viewing order.

---

## Security Rules

Before committing any screenshot, verify that it does not reveal:

- email address;
- Kaggle token;
- API key;
- tenant identifier;
- workspace identifier;
- browser cookies;
- signed URL;
- private account information;
- confidential bookmarks or browser tabs.

Crop unnecessary browser areas where practical.

---

## README Usage

Only high-value screenshots should be displayed in the main README.

Detailed execution screenshots should be embedded in the relevant file under:

```text
docs/
```

This prevents the main README from becoming excessively long.

---

## Current Screenshots

### Fabric Setup

Stored under:

```text
screenshots/fabric-setup/
```

### Data Ingestion

Stored under:

```text
screenshots/03-data-ingestion/
```

These demonstrate:

- successful notebook ingestion;
- all source files stored in OneLake;
- source-inventory validation.