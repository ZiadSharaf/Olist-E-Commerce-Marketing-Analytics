<p align="center">
  <img src="https://raw.githubusercontent.com/microsoft/PowerBI-Icons/main/SVG/Power-BI.svg" alt="Power BI" width="80">
</p>

<h1 align="center">Olist Analytics</h1>

<h3 align="center">E-Commerce &amp; Marketing Performance</h3>

<p align="center">
  Sales · Orders · Fulfillment · Customers · Payments · Marketing
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge" alt="Power BI">
  <img src="https://img.shields.io/badge/Power_Query-217346?style=for-the-badge" alt="Power Query">
  <img src="https://img.shields.io/badge/DAX-41666F?style=for-the-badge" alt="DAX">
  <img src="https://img.shields.io/badge/Kaggle-20BEFF?style=for-the-badge&amp;logo=kaggle&amp;logoColor=white" alt="Kaggle">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Fact_Tables-4-41666F?style=flat-square" alt="4 Fact Tables">
  <img src="https://img.shields.io/badge/Dimension_Tables-7-41666F?style=flat-square" alt="7 Dimension Tables">
  <img src="https://img.shields.io/badge/DAX_Measures-53-F2C811?style=flat-square" alt="53 DAX Measures">
  <img src="https://img.shields.io/badge/Report_Views-8-F2C811?style=flat-square" alt="8 Report Views">
</p>

<p align="center">
  <a href="#project-overview">Overview</a>
  &nbsp; | &nbsp;
  <a href="#data-model">Data Model</a>
  &nbsp; | &nbsp;
  <a href="#report-gallery">Report Gallery</a>
  &nbsp; | &nbsp;
  <a href="#dax-calculations">DAX</a>
  &nbsp; | &nbsp;
  <a href="#data-sources">Data Sources</a>
</p>

---

## Project Overview

A Power BI project that connects e-commerce operations and marketing lead data from Olist.

The report analyzes sales, orders, fulfillment, products, sellers, customers, payments, and marketing conversion.

The implementation includes data preparation with Power Query, dimensional modeling, and DAX calculations.

### Business Questions

- How do sales, order value, and order volume change over time?
- How long do order approval and delivery take?
- How many deliveries meet their estimated dates?
- Which product categories and seller locations contribute to item sales?
- How do purchasing patterns differ across customers and locations?
- How do customers use payment methods and installments?
- Which lead origins generate won leads, and how long does conversion take?

---

## Report Snapshot

Values displayed in the supplied report screenshots.

| Orders | Order Items | Unique Customers |
| :---: | :---: | :---: |
| __99.441K__ | __112.650K__ | __96.096K__ |

| Order Sales | Order Value Including Freight | Average Order Value Excluding Freight |
| :---: | :---: | :---: |
| __13.592M__ | __15.844M__ | __136.68__ |

| Average Delivery Days | Marketing Leads | Won Leads |
| :---: | :---: | :---: |
| __12.50__ | __8,000__ | __842__ |

---

## Data Sources

<p>
  <a href="https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce/data">
    <img src="https://img.shields.io/badge/Kaggle-E--Commerce_Dataset-20BEFF?style=for-the-badge&amp;logo=kaggle&amp;logoColor=white" alt="Olist E-Commerce Dataset">
  </a>
</p>

Orders, customers, products, sellers, order items, payments, and product category translations.

<p>
  <a href="https://www.kaggle.com/datasets/olistbr/marketing-funnel-olist">
    <img src="https://img.shields.io/badge/Kaggle-Marketing_Funnel-20BEFF?style=for-the-badge&amp;logo=kaggle&amp;logoColor=white" alt="Olist Marketing Funnel Dataset">
  </a>
</p>

Marketing-qualified leads and closed deals.

The marketing and e-commerce datasets connect through seller identifiers.

---

## Data Preparation

Data preparation was implemented in Power Query through __14 queries__.

| Area | Transformation |
| --- | --- |
| Data import | Read CSV files and assign column data types |
| Column selection | Retain the attributes required for analysis |
| Deduplication | Remove duplicate identifiers in the relevant dimension queries |
| Surrogate keys | Create numeric keys for dimension tables |
| Table integration | Merge fact records with dimension keys |
| Product categories | Join Portuguese categories with English translations |
| Geography | Convert Brazilian state codes into state names |
| Unknown sellers | Add an Unknown seller record with key -1 |
| Marketing integration | Combine qualified leads with closed deals |
| Lead status | Assign Won or Not Won based on the presence of a win date |
| Date and time keys | Create keys for order, shipping, and marketing events |

### Date and Time Dimensions

- __Dim_Date__ covers the date range found across the source tables.
- __Dim_Time__ contains 1,440 rows, representing each minute of the day.
- Calendar attributes support analysis by year, quarter, month, and weekday.
- Time attributes support analysis by hour, minute, AM/PM, and time band.

---

## Data Model

The model contains __4 fact tables__, __7 dimension tables__, and a table for DAX measures.

![Power BI Data Model](<images/Screenshot 2026-10-16 131245.png>)

<details>
<summary><strong>Explore the fact tables</strong></summary>

| Table | Purpose |
| --- | --- |
| Fact_Orders | Order status, customer references, timestamps, and order totals |
| Fact_Order_Items | Order items, product and seller references, prices, and freight |
| Fact_Order_Payments | Payment records, methods, installment counts, and payment values |
| Fact_Marketing_Leads | Lead origins, business attributes, status, and contact and win dates |

</details>

<details>
<summary><strong>Explore the dimension tables</strong></summary>

| Table | Purpose |
| --- | --- |
| Dim_Customers | Customer identifiers and locations |
| Dim_Products | Product identifiers and category names |
| Dim_Sellers | Seller identifiers and locations |
| Dim_Orders | Order identifiers shared across order-related tables |
| Dim_payment_type | Payment method categories |
| Dim_Date | Calendar dates and their attributes |
| Dim_Time | Time values, hours, minutes, AM/PM, and time bands |

</details>

### Date Relationships

Order analysis uses purchase date as its default date relationship. Marketing analysis uses first-contact date.

Inactive relationships support analysis by approval date, carrier handoff date, customer delivery date, estimated delivery date, and lead win date.

Relevant measures activate these relationships using `USERELATIONSHIP`.

---

## Report Gallery

Select a report view to explore its purpose and screenshot.

<details open>
<summary><strong>01 · Executive Overview</strong></summary>

### Executive Overview

Summarizes order volume, sales, order value, order items, and unique customers.

The view also shows yearly trends, delivery timeliness, and sales by order status.

![Executive Overview](<images/Screenshot 2026-10-16 131300.png>)

</details>

<details>
<summary><strong>02 · Sales &amp; Orders</strong></summary>

### Sales & Orders

Analyzes freight, average order value, items per order, and sales trends.

Orders are also analyzed by purchase time band and customer state.

![Sales and Orders](<images/Screenshot 2026-10-16 131317.png>)

</details>

<details>
<summary><strong>03 · Order Fulfillment</strong></summary>

### Order Fulfillment

Tracks delivered and canceled orders, approval time, delivery time, and on-time delivery.

The view compares delivery performance across customer cities and shows order status trends.

![Order Fulfillment](<images/Screenshot 2026-10-16 131337.png>)

</details>

<details>
<summary><strong>04 · Products &amp; Sellers</strong></summary>

### Products & Sellers

Analyzes item sales, item prices, product counts, and seller activity.

Product categories are compared by sales and item counts. Seller locations are compared by item sales.

![Products and Sellers](<images/Screenshot 2026-10-16 131354.png>)

</details>

<details>
<summary><strong>05 · Customer Analysis</strong></summary>

### Customer Analysis

Examines unique customers, repeat customers, and orders per customer.

The view compares customer cities and states by sales and order counts.

![Customer Analysis](<images/Screenshot 2026-10-16 131640.png>)

</details>

<details>
<summary><strong>06 · Payments Analysis</strong></summary>

### Payments Analysis

Analyzes payment values, transaction counts, paid orders, and installments.

The view compares payment methods and displays the difference between recorded payment value and order value.

![Payments Analysis](<images/Screenshot 2026-10-16 131654.png>)

</details>

<details>
<summary><strong>07 · Marketing Leads</strong></summary>

### Marketing Leads

Tracks total leads, won leads, leads without a recorded win, conversion, and average time to win.

Won leads are analyzed by business segment, business type, lead type, and win date.

![Marketing Leads](<images/Screenshot 2026-10-16 131744.png>)

</details>

<details>
<summary><strong>08 · Marketing Lead Performance</strong></summary>

### Marketing Lead Performance

Analyzes lead origins, first-contact trends, and conversion by origin.

A matrix displays lead counts and conversion calculations across business segments and lead types.

![Marketing Lead Performance](<images/Screenshot 2026-10-16 131755.png>)

</details>

---

## DAX Calculations

<p>
  <img src="https://img.shields.io/badge/Measures-53-41666F?style=for-the-badge" alt="53 Measures">
  <img src="https://img.shields.io/badge/Display_Folders-14-41666F?style=for-the-badge" alt="14 Display Folders">
  <img src="https://img.shields.io/badge/Calculated_Columns-2-F2C811?style=for-the-badge" alt="2 Calculated Columns">
</p>

### Calculated Columns

Two calculated columns aggregate item values for each order in `Fact_Orders`.

| Column | Calculation |
| --- | --- |
| order_price | Sum of item prices for the matching order_key |
| freight_price | Sum of item freight values for the matching order_key |

### Main Measures

| Measure | Definition |
| --- | --- |
| Total Orders | Distinct order keys in Fact_Orders |
| Order Sales | Sum of order_price |
| Order Freight | Sum of freight_price |
| Order Value | Order Sales plus Order Freight |
| Average Order Value | Order Sales divided by Total Orders, excluding freight |
| Average Order Value Incl Freight | Order Value divided by Total Orders |
| Total Order Items | Number of rows in Fact_Order_Items |
| Unique Customers | Distinct customer_unique_id values in Dim_Customers |
| Repeat Customers | Customers with more than one order in the current order context |
| Average Delivery Days | Average calendar-day difference between purchase and delivery for delivered orders |
| On Time Delivery Rate | On-time delivered orders divided by delivered orders |
| Total Payment Value | Sum of recorded payment values |
| Lead Conversion Rate | Won Leads divided by Total Leads |
| Average Days to Win | Average calendar-day difference between first contact and win date |

### DAX Functions Used

`CALCULATE` · `FILTER` · `SUMX` · `AVERAGEX` · `DISTINCTCOUNT`

`DIVIDE` · `LOOKUPVALUE` · `USERELATIONSHIP` · `TREATAS`

---

## Skills Demonstrated

| Area | Implementation |
| --- | --- |
| Data preparation | Import, transform, and combine CSV data using Power Query |
| Dimensional modeling | Build and connect multiple fact and dimension tables |
| Data integration | Connect e-commerce and marketing datasets |
| DAX development | Create measures and calculated columns |
| Date analysis | Analyze business events through different date relationships |
| Business reporting | Present metrics across sales, operations, customers, payments, and marketing |

---

## Credits

- Datasets published by [Olist on Kaggle](https://www.kaggle.com/olistbr).
- Power BI icon from [Microsoft Power BI Icons](https://github.com/microsoft/PowerBI-Icons).
- Technology badges provided by [Shields.io](https://shields.io).

Dataset attribution and license details are available on the source dataset pages.

<p align="center">
  <a href="#olist-analytics">Back to top</a>
</p>
