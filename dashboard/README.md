# Olist E-Commerce Analytics Dashboard

This folder contains the final Power BI reporting layer for the **Microsoft Fabric Olist E-Commerce Analytics** project.

The report is built on top of the curated Microsoft Fabric semantic model and presents business-facing analytics across revenue, customers, logistics, payments, and customer experience.

The final report contains **five completed and QA-validated pages**.

---

## Dashboard Scope

| Page                                | Business Focus                                         | KPI Cards | Main Visuals |
| ----------------------------------- | ------------------------------------------------------ | --------: | -----------: |
| **01 Executive Overview**     | Overall marketplace performance                        |         6 |            6 |
| **02 Sales & Revenue**        | Revenue trends, categories, sellers, and concentration |         6 |            6 |
| **03 Customer Intelligence**  | Customer growth, repeat behavior, value, and frequency |         6 |            6 |
| **04 Operations & Logistics** | Delivery performance, delays, and freight analysis     |         6 |            6 |
| **05 Payments & Reviews**     | Payment behavior and customer satisfaction             |         6 |            6 |

Common page slicers:

- **Year**
- **Month**
- **Customer State**

All pages use consistent navigation, KPI-card styling, visual containers, typography, and interaction patterns.

---

## Report Files

```text
dashboard/
├── Icon Set/
├── Complete_Dashboard_Planning_Matrix.xlsx
├── rpt_olist_ecommerce_analytics.pbix
└── README.md
```

### `rpt_olist_ecommerce_analytics.pbix`

Final five-page Power BI report connected to the Microsoft Fabric semantic model.

### `Complete_Dashboard_Planning_Matrix.xlsx`

Final dashboard specification containing:

- page-level objectives;
- KPI inventory;
- visual inventory;
- measures used;
- source tables and fields;
- visual types;
- placements;
- priorities;
- KPI dictionary;
- final dashboard summary.

### `Icon Set/`

Reusable icons used to maintain a consistent visual language across dashboard navigation and KPI cards.

---

# 01 — Executive Overview

**Purpose:** Provide leadership with a concise view of overall marketplace performance.

### KPIs

- Total GMV
- Total Orders
- Active Customers
- Average Order Value
- Delivery Rate
- Average Review Score

### Visuals

- Monthly GMV and Order Trend
- Orders by Status
- Delivery Performance
- Top 6 States by Revenue
- Top 10 Product Categories by Revenue
- Revenue by Payment Method

![Executive Overview](<../screenshots/10-dashboard/01%20Executive%20Overview.png>)

---

# 02 — Sales & Revenue

**Purpose:** Explain where revenue is generated, how it changes over time, and which products and sellers drive commercial performance.

### KPIs

- Total GMV
- Total Orders
- Average Order Value
- GMV YoY %
- Active Products
- Active Sellers

### Visuals

- Monthly Revenue
- Top 6 States by Revenue
- Top 10 Sellers by Revenue
- Top 10 Product Categories by Revenue
- Category Performance Matrix
- Revenue Pareto Analysis by Product Category

The Pareto visual uses category ranking and cumulative GMV measures to analyze revenue concentration.

![Sales & Revenue](<../screenshots/10-dashboard/02%20Sales%20%26%20Revenue.png>)

---

# 03 — Customer Intelligence

**Purpose:** Analyze customer acquisition, repeat purchasing, geography, value, and order frequency.

### KPIs

- Active Customers
- Repeat Customers
- Repeat Customer Rate
- Average Orders per Customer
- Average GMV per Customer
- New Customers

### Visuals

- Monthly Customer Growth Trend
- Top 10 States by Active Customers
- Top 10 States by Customer Value
- Customer Order Frequency
- Customer Value Distribution
- Customer Value vs Order Frequency

Disconnected helper tables are used for the order-frequency and customer-value-band distributions.

![Customer Intelligence](<../screenshots/10-dashboard/03%20Customer%20Intelligence.png>)

---

# 04 — Operations & Logistics

**Purpose:** Monitor fulfilment reliability, delivery speed, delay severity, geography, and freight behavior.

### KPIs

- Delivery Rate
- On-Time Delivery Rate
- Late Delivery Rate
- Average Delivery Days
- Average Delivery Delay Days
- Average Approval Hours

### Visuals

- Monthly Delivery Performance Trend
- Bottom 10 States by On-Time Delivery Rate
- Delivery Delay Distribution
- Average Delivery Time Trend
- Freight Cost vs Delivery Time by State
- Order Delivery Outcome

The page highlights operational problem areas rather than only showing high-performing regions.

![Operations & Logistics](<../screenshots/10-dashboard/04%20Operations%20%26%20Logistics.png>)

---

# 05 — Payments & Reviews

**Purpose:** Analyze transaction behavior, installment usage, review patterns, and customer satisfaction.

### KPIs

- Payment Fact Value
- Payment Transactions
- Average Installments
- Average Review Score
- High Rating Rate
- Low Rating Rate

### Visuals

- Payment Value by Method
- Customer Review Score Distribution
- Customer Satisfaction Breakdown
- Top States by Customer Satisfaction
- Monthly Customer Satisfaction Trend
- Payment Transactions by Installments

The satisfaction breakdown classifies reviews into:

- **High:** 4–5 stars
- **Neutral:** 3 stars
- **Low:** 1–2 stars

![Payments & Reviews](<../screenshots/10-dashboard/05%20Payments%20%26%20Customer%20Experience.png>)

---

## Semantic Model

The report uses the project's Direct Lake semantic model built on the Gold dimensional layer.

### Dimensions

- `dim_date`
- `dim_customer`
- `dim_product`
- `dim_seller`

### Facts

- `fact_order`
- `fact_order_item`
- `fact_payment`

The model uses one-to-many, single-direction relationships from dimensions to facts.

A dedicated `_Measures` table organizes reusable DAX measures into business folders such as:

```text
Customers
Delivery
Orders
Payments
Products
Revenue
Reviews
Sellers
Time Intelligence
```

---

## Dashboard Design

The report uses a consistent visual system across all five pages.

### Theme

- Primary accent: deep Olist-inspired purple
- Light blue page background
- White rounded visual containers
- Soft shadows
- Semantic green/orange/red accents where business meaning requires them

### Layout

Each page follows a common structure:

```text
Header + Global Slicers
        ↓
Navigation Bar
        ↓
Six KPI Cards
        ↓
Business Visual Grid
```

### Navigation

The final report navigation is:

```text
Executive Overview
Sales & Revenue
Customer Intelligence
Operations & Logistics
Payments & Reviews
```

---

## Dashboard Interaction Standards

The report was QA-tested for:

- Year slicer behavior;
- Month slicer behavior;
- Customer State slicer behavior;
- KPI response to filter context;
- chronological sorting of monthly trends;
- Top-N / Bottom-N ranking logic;
- cross-filtering between visuals;
- measure formatting;
- tooltip behavior;
- consistent navigation;
- visual alignment and styling.

---

## Key Analytical Features

The final report demonstrates more than basic charting.

Examples include:

- Year-over-year GMV analysis;
- category-level Pareto / cumulative revenue analysis;
- repeat-customer analysis;
- dynamic new-customer calculation;
- customer order-frequency bucketing;
- customer-value segmentation;
- delivery-delay bands;
- mutually exclusive delivery-outcome categories;
- freight-cost vs delivery-time analysis;
- payment-installment analysis;
- customer satisfaction grouping.

---

## Screenshots

Final dashboard screenshots are stored in:

```text
screenshots/
└── 10-dashboard/
    ├── 01 Executive Overview.png
    ├── 02 Sales & Revenue.png
    ├── 03 Customer Intelligence.png
    ├── 04 Operations & Logistics.png
    └── 05 Payments & Customer Experience.png
```

---

## Final Status

| Component           | Status          |
| ------------------- | --------------- |
| Dashboard pages     | ✅ Complete     |
| KPI measures        | ✅ Complete     |
| Analytical visuals  | ✅ Complete     |
| Navigation          | ✅ Complete     |
| Global slicers      | ✅ Complete     |
| Visual interactions | ✅ QA validated |
| Formatting          | ✅ Complete     |
| Screenshots         | ✅ Complete     |
| Power BI report     | ✅ Final        |

The previously planned **Fabric Operations** dashboard page was intentionally removed from the final reporting scope. Platform engineering, audit, profiling, data-quality, and pipeline capabilities are documented separately in the project repository rather than duplicated in the business-facing Power BI report.
