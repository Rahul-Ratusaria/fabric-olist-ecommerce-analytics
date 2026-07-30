# Gold Layer

## Purpose

Transform standardized silver entities into a business-ready model for SQL analytics and Power BI.


## Inputs

- `silver_customers`
- `silver_orders`
- `silver_order_items`
- `silver_products`
- `silver_sellers`
- `silver_order_payments`
- `silver_order_reviews`
- `silver_geolocation_zip`

## Planned Outputs

### Dimensions

- `dim_date`
- `dim_customer`
- `dim_product`
- `dim_seller`

### Facts

- `fact_order`
- `fact_order_item`
- `fact_payment`

## Design Pattern

The gold layer follows a star-schema design.

Dimension table provides descriptive attributes for filtering and grouping.

Fact tables retain measurable business events at explicitly documented grains.

## Table Grains

| Table | Grain |
| -- | -- |
| `dim_date` | One row per calendar date |
| `dim_customer` | One row per customer ID |
| `dim_product` | One row per product ID |
| `dim_seller` | One row per seller ID |
| `fact_order` | One row per order |
| `fact_order_item` | One row per order and item sequence |
| `fact_payment` | One row per order and payment sequence |

## Key Design Decisions

- separate facts prevent item-payment multiplication.
- dimensions use deterministic integer surrogate keys.
- purchase date is the primary reporting-customer analysis.
- `customer_unique_id` is retained for repeat-customer analysis.
- monetary fields remain in Brazilian real.
- GMV is not interpreted as profit.
- required filter attributes are materialized in the gold dimension.

## Status

Design completed. Implementation in progress.