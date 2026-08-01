# Microsoft Fabric Pipeline

## Objective

Automate execution of the complete analytics platform.

The pipeline replaces manual notebook execution.

The pipeline currently orchestrates five notebook activities.

Pipeline Flow

Landing

↓

Profiling

↓

Bronze

↓

Silver

↓

Gold

## Expected Benefits

- automation;
- dependency management;
- monitoring;
- scheduling;
- retry support;
- production readiness.

Notebook activities execute sequentially using Success dependencies.

The orchestration layer will later be extended with monitoring and scheduling.

## Evidence

![Pipeline](../screenshots/08-pipeline/01-pipeline-design.png)

![Notebook Properties](../screenshots/08-pipeline/02-notebook-properties.png)

![Dependencies](../screenshots/08-pipeline/03-dependency-view.png)