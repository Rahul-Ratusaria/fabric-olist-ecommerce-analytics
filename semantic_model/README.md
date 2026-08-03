# Fabric Semantic Model

## Objective

The Semantic Model provides the business layer between the Gold Lakehouse tables and the Power BI reports.

It centralizes:

- relationships;
- DAX measures;
- hierarchies;
- KPIs;
- formatting;
- business definitions.

The model ensures all reports use a consistent analytical layer.

## Gold Tables

Dimensions

- dim_date
- dim_customer
- dim_product
- dim_seller

Facts

- fact_order
- fact_order_item
- fact_payment

Status

In Progress