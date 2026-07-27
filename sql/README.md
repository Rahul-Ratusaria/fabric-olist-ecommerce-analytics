# SQL Scripts

This folder will contain SQL used for validation, dimensional modelling, reconciliation and business analysis.

The SQL will primarily be executed through the Lakehouse SQL analytics endpoint or an optional Fabric Warehouse.

---

## Planned SQL Files

| File | Purpose | Status |
|---|---|---|
| `validation.sql` | Key, duplicate, null and reconciliation checks | Planned |
| `analytical_queries.sql` | Business analysis and dashboard validation | Planned |
| `warehouse_ddl.sql` | Optional Warehouse fact and dimension definitions | Planned |
| `reconciliation.sql` | Bronze, Silver, Gold and semantic-model reconciliation | Planned |

---

## SQL Standards

SQL scripts should:

- use meaningful comments;
- state the expected table grain;
- avoid `SELECT *` in final analytical queries;
- use consistent indentation;
- protect divisions with `NULLIF` or equivalent logic;
- clearly distinguish item, order and payment grains;
- avoid joining order items directly to payment records without aggregation;
- include validation queries after transformation logic.

---

## Planned Analytical Queries

The project will include queries for:

- monthly GMV and order trends;
- average order value;
- category contribution;
- seller rankings;
- customer-state performance;
- order-status distribution;
- delivery performance;
- late-delivery rate;
- review-score distribution;
- delivery-delay and review relationship;
- payment-method analysis;
- instalment behaviour;
- source-to-target reconciliation.

---

## Metric Boundary

Item-price totals will be labelled as:

```text
Gross Merchandise Value
```

They will not be labelled as profit because product cost, commission, tax and operating expenses are not included in the dataset.