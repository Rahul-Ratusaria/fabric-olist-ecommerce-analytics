# Power BI Dashboard

## Objective

Provide an executive-friendly analytical experience over the Microsoft
Fabric Gold model and semantic layer.

The final report contains **five completed pages** with consistent
navigation, global filters, KPI cards, and domain-specific analytical
visuals.

## Design System

The report uses a consistent visual language across all pages:

-   light blue page background;
-   white rounded visual containers;
-   dark purple as the primary analytical color;
-   colored KPI accents;
-   icon-based left navigation;
-   horizontal page navigation;
-   consistent Year, Month, and Customer State slicers;
-   compact executive layout.

Dashboard screenshots are stored under:

``` text
screenshots/10-dashboard/
```

------------------------------------------------------------------------

## Page 1 --- Executive Overview

![Executive
Overview](../screenshots/10-dashboard/01%20Executive%20Overview.png)

### KPIs

-   Total GMV
-   Total Orders
-   Active Customers
-   Average Order Value
-   Delivery Rate
-   Average Review Score

### Visuals

-   Monthly GMV and Order Trend
-   Orders by Status
-   Delivery Performance
-   Average Delivery Days
-   Cancellation Rate
-   Top States by Revenue
-   Top Product Categories by Revenue
-   Revenue by Payment Method

### Purpose

Provide leadership with a single-page view of commercial scale,
customers, fulfillment, product mix, geography, and payment behavior.

------------------------------------------------------------------------

## Page 2 --- Sales & Revenue

![Sales &
Revenue](../screenshots/10-dashboard/02%20Sales%20%26%20Revenue.png)

### KPIs

-   Total GMV
-   Total Orders
-   Average Order Value
-   GMV YoY %
-   Active Products
-   Active Sellers

### Visuals

-   Monthly Revenue
-   Top States by Revenue
-   Top Sellers by Revenue
-   Top Product Categories by Revenue
-   Product/category performance table
-   Revenue Pareto Analysis by Product Category

### Purpose

Analyze revenue trends and identify the products, categories, sellers,
and states driving commercial performance.

------------------------------------------------------------------------

## Page 3 --- Customer Intelligence

![Customer
Intelligence](../screenshots/10-dashboard/03%20Customer%20Intelligence.png)

### KPIs

-   Active Customers
-   Repeat Customers
-   Repeat Customer Rate
-   Average Orders per Customer
-   Average GMV per Customer
-   New Customers

### Visuals

-   Monthly Customer Growth Trend
-   Top States by Active Customers
-   Top States by Customer Value
-   Customer Order Frequency
-   Customer Value Distribution
-   Customer Value vs Order Frequency

### Purpose

Understand customer acquisition, repeat behavior, order frequency,
geographic concentration, and customer value.

------------------------------------------------------------------------

## Page 4 --- Operations & Logistics

![Operations &
Logistics](../screenshots/10-dashboard/04%20Operations%20%26%20Logistics.png)

### KPIs

-   Delivery Rate
-   On-Time Delivery Rate
-   Late Delivery Rate
-   Average Delivery Days
-   Average Delivery Delay Days
-   Average Approval Hours

### Visuals

-   Monthly Delivery Performance Trend
-   Bottom States by On-Time Delivery Rate
-   Delivery Delay Distribution
-   Average Delivery Time Trend
-   Freight Cost vs Delivery Time by State
-   Order Delivery Outcome

### Purpose

Monitor fulfillment reliability, delivery speed, delay patterns,
geographic operational performance, and freight-versus-delivery
behavior.

------------------------------------------------------------------------

## Page 5 --- Payments & Reviews

![Payments &
Reviews](../screenshots/10-dashboard/05%20Payments%20%26%20Customer%20Experience.png)

### KPIs

-   Payment Fact Value
-   Payment Transactions
-   Average Installments
-   Average Review Score
-   High Rating Rate
-   Low Rating Rate

### Visuals

-   Payment Value by Method
-   Customer Review Score Distribution
-   Customer Satisfaction Breakdown
-   Top States by Customer Satisfaction
-   Monthly Customer Satisfaction Trend
-   Payment Transactions by Installments

### Purpose

Combine payment behavior and customer-feedback analysis to understand
transaction patterns, installment usage, review outcomes, and
satisfaction trends.

------------------------------------------------------------------------

## Navigation & Interactivity

The final report includes:

-   page-navigation buttons;
-   left-side icon navigation;
-   active-page highlighting;
-   Year slicer;
-   Month slicer;
-   Customer State slicer;
-   visual cross-filtering and tooltips.

## Final Scope

An earlier Fabric Operations reporting concept was not retained as a
sixth business dashboard page. Fabric engineering, orchestration,
data-quality, and architecture evidence is documented separately in the
repository rather than duplicated in the business report.

## Result

**Status: Complete**

The final Power BI solution contains five polished analytical pages
covering executive performance, sales, customers, operations, payments,
and reviews.
