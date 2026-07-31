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

## Implemented Dimensions

The Gold implementation currently contains:

- `dim_date`;
- `dim_customer`;
- `dim_product`;
- `dim_seller`.

## Date Dimension

`dim_date` contains one row per calendar date across the full analytical date range found in the Silver tables.

Attributes include:

- year;
- quarter;
- month;
- week;
- day;
- weekday;
- weekend flag;
- year-month sorting fields.

The integer `date_key` uses the `YYYYMMDD` format.

## Customer Dimension

`dim_customer` contains one row per `customer_id`.

It retains `customer_unique_id` for persistent-customer analysis.

Enrichments include:

- first order date;
- last order date;
- lifetime distinct order count;
- new/repeat classification;
- ZIP-level coordinates.

## Product Dimension

`dim_product` contains one row per product.

It includes:

- Portuguese category;
- English category;
- translation status;
- descriptive text-length attributes;
- photo count;
- weight;
- dimensions;
- volume;
- density.

## Seller Dimension

`dim_seller` contains one row per seller and includes seller geography and ZIP-level coordinates.

## Surrogate Keys

Integer surrogate keys are generated deterministically by ordering the natural key and assigning `row_number()`.

This approach is suitable for the static portfolio dataset.

A production incremental solution would use a persistent key-mapping strategy, identity key or merge process.

## Dimension Validation

Every dimension is tested for:

- expected row count;
- natural-key uniqueness;
- surrogate-key uniqueness;
- null surrogate keys.

Results are stored in:

- `audit_gold_dimension_load`

## Evidence

![Gold dimensions](../screenshots/07-gold-layer/01-gold-dimensions.png)

![Date dimension](../screenshots/07-gold-layer/02-date-dimension.png)

![Customer dimension](../screenshots/07-gold-layer/03-customer-dimension.png)

![Product dimension](../screenshots/07-gold-layer/04-product-dimension.png)

![Seller dimension](../screenshots/07-gold-layer/05-seller-dimension.png)

![Dimension audit](../screenshots/07-gold-layer/06-dimension-audit.png)