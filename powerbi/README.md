# Power BI Semantic Model and Dashboard

This folder contains Power BI documentation, DAX definitions, visual specifications and report screenshots for the Olist analytics project.

---

## Planned Fabric Items

### Semantic Model

```text
sm_olist_analytics
```

### Report

```text
Olist E-Commerce Analytics Dashboard
```

---

## Planned Model Tables

### Dimensions

```text
dim_date
dim_customer
dim_product
dim_seller
```

### Facts

```text
fact_order
fact_order_item
fact_payment
```

### Audit Tables

```text
audit_ingestion
audit_data_quality
audit_pipeline_run
```

---

## Planned Relationships

```text
dim_date[date_key]
    1 ─── * fact_order[order_date_key]

dim_date[date_key]
    1 ─── * fact_order_item[order_date_key]

dim_customer[customer_id]
    1 ─── * fact_order[customer_id]

dim_product[product_id]
    1 ─── * fact_order_item[product_id]

dim_seller[seller_id]
    1 ─── * fact_order_item[seller_id]
```

Relationships will use single-direction filtering wherever possible.

---

## Planned Dashboard Pages

### 1. Executive Overview

Key indicators:

- Total GMV
- Orders
- Average order value
- Customers
- Late-delivery rate
- Average review score

Main visuals:

- monthly performance trend;
- top categories;
- customer-state performance;
- order-status distribution;
- on-time versus late review comparison.

### 2. Sales and Product Performance

Main analysis:

- category contribution;
- product rankings;
- seller performance;
- seller concentration;
- freight ratio;
- average item price.

### 3. Customer and Payment Analysis

Main analysis:

- new and repeat customers;
- customer geography;
- orders per customer;
- payment-type mix;
- instalment distribution;
- optional RFM segmentation.

### 4. Logistics and Customer Experience

Main analysis:

- average and median delivery duration;
- late-delivery rate;
- delay buckets;
- seller and state delay analysis;
- review-score distribution;
- delay and review relationship.

### 5. Data Quality and Monitoring

Main analysis:

- latest pipeline run;
- test pass and failure counts;
- critical-quality failures;
- ingestion row counts;
- source-to-target reconciliation;
- data refresh timestamp.

---

## Planned Power BI Files

| File | Purpose |
|---|---|
| `dax-measures.md` | DAX definitions and measure descriptions |
| `visual-specification.md` | Page-by-page visual design |
| `model-documentation.md` | Relationships, grains and table descriptions |
| `screenshots/` | Final report-page screenshots |

A `.pbix` or `.pbip` file may be included if export is supported and the file does not expose credentials or unsupported data connections.

---

## Dashboard Standards

The report will:

- use a consistent 16:9 layout;
- show the data period;
- use Brazilian real notation for source monetary values;
- distinguish GMV from profit;
- provide clear KPI definitions;
- avoid misleading cross-filtering;
- include a reset-filters option;
- use accessible visual titles and labels;
- include a dedicated data-quality page.

---

## Validation

Every major Power BI measure will be reconciled against SQL or Spark output before the dashboard is considered complete.