# Enterprise E-Commerce Analytics Platform

## Project Overview

This project implements an end-to-end e-commerce analytics platform
using **Microsoft Fabric**, **OneLake**, a **Medallion Architecture**, a
dimensional Gold model, and **Power BI**.

The platform uses the public Olist e-commerce source files to
demonstrate a complete analytics lifecycle from raw-file ingestion
through data quality, transformation, dimensional modeling,
orchestration, semantic modeling, and executive reporting.

## Business Problem

The source data is distributed across multiple CSV files containing
customer, order, product, seller, payment, review, order-item, and
geolocation information.

Without a centralized analytical platform, business users do not have a
consistent reporting layer for analyzing:

- sales and revenue performance;
- customer purchasing behaviour;
- product and seller performance;
- delivery efficiency;
- payments;
- customer reviews and satisfaction.

## Objective

Build a reusable Microsoft Fabric analytics solution that:

1. ingests raw Olist data into OneLake;
2. profiles source quality before transformation;
3. implements Bronze, Silver, and Gold layers;
4. quarantines invalid records instead of silently discarding them;
5. builds a dimensional analytical model;
6. orchestrates processing through a Fabric Data Pipeline;
7. exposes governed business measures through a Power BI semantic
   model;
8. delivers an interactive five-page Power BI dashboard;
9. documents the implementation for reproducibility and portfolio
   review.

## Business Goals

- Analyze overall sales performance.
- Monitor customer purchasing behavior.
- Evaluate seller performance.
- Identify top-performing products and categories.
- Monitor delivery efficiency and delays.
- Analyze payments and installment behavior.
- Analyze customer reviews and satisfaction.
- Build reusable data pipelines.
- Demonstrate enterprise-style data engineering and BI practices.

## Success Criteria

---

  Area                    Success Criterion       Final Status

---

  Ingestion               Automated ingestion of  Complete
                          the Olist source files

  Data Quality            Source profiling,       Complete
                          validation, quarantine,
                          and audit controls

  Architecture            Bronze → Silver → Gold  Complete
                          Medallion Architecture

  Modeling                Dimensional model with  Complete
                          separate analytical
    fact grains

  Orchestration           Sequential Fabric       Complete
                          pipeline with success
    dependencies

  Semantic Layer          Relationships,          Complete
                          measures, KPI
    organization, and
    formatting

  Reporting               Five-page interactive   Complete
                          Power BI dashboard

Documentation           GitHub-ready            Complete
                          implementation
    documentation
--------------------------------------------

## Stakeholders

- CEO / executive leadership
- Sales manager
- Operations manager
- Product team
- Customer success team
- Analytics / data engineering team

## Final Analytical Areas

The completed reporting solution covers:

1. Executive Overview
2. Sales & Revenue
3. Customer Intelligence
4. Operations & Logistics
5. Payments & Reviews

## Result

The project delivers a complete portfolio-grade Microsoft Fabric
analytics solution spanning ingestion, data engineering, data quality,
dimensional modeling, orchestration, semantic modeling, and Power BI
reporting.
