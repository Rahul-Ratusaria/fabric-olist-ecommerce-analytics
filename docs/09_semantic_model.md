# Fabric Semantic Model

## Objective

Create the governed business layer used by Power BI over the completed
Gold dimensional model.

## Source Model

The semantic layer is built on the Gold star-schema tables.

### Dimensions

-   `dim_date`
-   `dim_customer`
-   `dim_product`
-   `dim_seller`

### Facts

-   `fact_order`
-   `fact_order_item`
-   `fact_payment`

The facts remain separate because they represent different analytical
grains. This prevents item and payment records from multiplying each
other and protects business measures from double counting.

## Relationship Design

The model follows dimensional-modeling principles:

-   one-to-many relationships from dimensions to facts;
-   single-direction filtering;
-   date filtering through `dim_date`;
-   customer filtering through `dim_customer`;
-   product and seller filtering at the item grain;
-   fact tables are not directly joined to one another for reporting.

## Measure Organization

Business measures are centralized under the `_Measures` table and
organized into display folders.

``` text
_Measures
├── Customers
├── Delivery
├── Orders
├── Payments
├── Products
├── Revenue
├── Reviews
├── sellers
└── Time Intelligence
```

## Core Measure Areas

### Revenue

Examples include:

-   Total GMV
-   Average Order Value
-   Total Freight
-   Total Payment
-   Category Revenue Rank
-   Cumulative Category GMV
-   Cumulative Category GMV %

### Orders

-   Total Orders
-   Delivered Orders
-   Cancelled Orders
-   Delivery Rate
-   Cancellation Rate

### Customers

-   Total Customers
-   Active Customers
-   Repeat Customers
-   Repeat Customer Rate

Additional customer measures support new-customer, order-frequency, and
customer-value analysis in the report.

### Products

-   Active Products
-   Item GMV
-   Items Sold
-   Average Item Price
-   Average Items per Order
-   Item Freight
-   Average Freight per Item

### Sellers

-   Active Sellers
-   Seller GMV
-   Average GMV per Seller
-   Average Items per Seller

### Delivery

-   Average Approval Hours
-   Average Delivery Days
-   Average Delivery Delay Days
-   On-Time Deliveries
-   On-Time Delivery Rate
-   Late Deliveries
-   Late Delivery Rate
-   Average Freight Share

### Payments

-   Payment Fact Value
-   Payment Transactions
-   Average Payment Transaction
-   Average Installments
-   Installment Transactions
-   Installment Usage Rate

### Reviews

-   Average Review Score
-   Reviewed Orders
-   Review Coverage Rate
-   High-Rated Orders
-   High Rating Rate
-   Low-Rated Orders
-   Low Rating Rate

### Time Intelligence

-   GMV Previous Year
-   GMV YoY %
-   GMV YoY Change
-   GMV YTD
-   Orders Previous Year
-   Orders YoY %
-   Orders YoY Change
-   Orders YTD

## Report Filtering

The report uses common business filters including:

-   Year
-   Month
-   Customer State

These filters are reused across report pages to provide a consistent
analytical experience.

## Formatting

Measures are formatted according to business meaning:

-   currency for GMV, payment, freight, and value measures;
-   percentages for rates;
-   whole-number or abbreviated formats for counts;
-   decimal formats for averages and duration metrics.

## Reporting Role

The semantic model supports the five completed report pages:

1.  Executive Overview
2.  Sales & Revenue
3.  Customer Intelligence
4.  Operations & Logistics
5.  Payments & Reviews

## Result

**Status: Complete**

The semantic model provides a reusable business layer over the Gold star
schema with organized measures, consistent filtering, dimensional
relationships, and KPI logic used by the final Power BI report.
