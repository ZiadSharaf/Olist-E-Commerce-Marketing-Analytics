# 🛒 Olist E-Commerce & Marketing Analytics

## 📌 Project Overview

This project analyzes e-commerce operations and marketing leads using two datasets published by Olist.

The Power BI report covers sales, orders, fulfillment, products, sellers, customers, payments, and marketing conversion.

The project includes data preparation with Power Query, dimensional modeling, and DAX calculations across eight report views.

---

## 🎯 Project Objectives

- Track sales, order value, and order volume over time.
- Analyze delivery performance and order fulfillment.
- Compare product categories and seller locations.
- Understand customer purchasing behavior.
- Analyze payment methods and installments.
- Track marketing leads, conversion, and time to win.

---

## 🗂️ Data Sources

The project uses two datasets published by Olist on Kaggle.

| Dataset | Main Data |
| --- | --- |
| [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce/data) | Orders, customers, products, sellers, order items, payments, and product category translations |
| [Marketing Funnel by Olist](https://www.kaggle.com/datasets/olistbr/marketing-funnel-olist) | Marketing-qualified leads and closed deals |

The marketing and e-commerce datasets connect through seller identifiers.

---

## 🛠️ Tools & Technologies

- __Power BI Desktop__ for data modeling and report development.
- __Power Query / M__ for data preparation and transformation.
- __DAX__ for measures and calculated columns.

---

## 🧹 Data Cleaning & Transformation

Data preparation was implemented through __14 Power Query queries__.

1. __Imported CSV files__ and assigned column data types.
2. __Selected the required columns__ for reporting and analysis.
3. __Removed duplicate identifiers__ in the relevant customer, order, payment-type, and lead dimension queries.
4. __Created surrogate keys__ for dimension tables.
5. __Merged fact tables with dimensions__ to retrieve their corresponding keys.
6. __Translated product categories__ from Portuguese into English.
7. __Handled missing category translations__ by replacing them with `unknown`.
8. __Converted Brazilian state codes__ into state names.
9. __Added an Unknown seller record__ with a key of `-1`.
10. __Combined marketing-qualified leads with closed deals__ using `mql_id`.
11. __Classified leads as Won or Not Won__ based on the presence of a win date.
12. __Created date and time keys__ for order, shipping, and marketing events.

### 📅 Date Dimension

`Dim_Date` covers the date range found across the source tables.

It includes:

- Date key and date.
- Year and quarter.
- Month number and month name.
- Weekday number and weekday name.

### 🕒 Time Dimension

`Dim_Time` contains __1,440 rows__, representing each minute of the day.

It includes:

- Time key and time.
- Hour and minute.
- AM/PM.
- Morning, Afternoon, Evening, and Night time bands.

---

## 🧱 Data Modeling

The dimensional model contains:

- __4 Fact Tables__
- __7 Dimension Tables__
- __1 DAX Measures Table__

### 📦 Fact Tables

| Table | Purpose |
| --- | --- |
| Fact_Orders | Order status, customer references, timestamps, and order totals |
| Fact_Order_Items | Order items, product and seller references, prices, and freight |
| Fact_Order_Payments | Payment records, payment methods, installment counts, and payment values |
| Fact_Marketing_Leads | Lead origins, business attributes, lead status, and contact and win dates |

### 🗃️ Dimension Tables

| Table | Purpose |
| --- | --- |
| Dim_Customers | Customer identifiers and locations |
| Dim_Products | Product identifiers and category names |
| Dim_Sellers | Seller identifiers and locations |
| Dim_Orders | Order identifiers shared across order-related tables |
| Dim_payment_type | Payment method categories |
| Dim_Date | Calendar dates and their attributes |
| Dim_Time | Time values, hours, minutes, AM/PM, and time bands |

### 🔗 Relationships

- `Dim_Orders` connects orders, order items, and payment records.
- `Dim_Customers` connects customer attributes to orders.
- `Dim_Products` and `Dim_Sellers` connect to order items.
- `Dim_payment_type` connects to payment records.
- `Dim_Sellers` also connects to marketing leads.
- `Dim_Date` and `Dim_Time` support analysis across business events.

Order analysis uses __purchase date__ as its default date relationship.

Marketing analysis uses __first-contact date__.

Inactive relationships support analysis by approval date, carrier handoff date, customer delivery date, estimated delivery date, and lead win date. Relevant measures activate these relationships using `USERELATIONSHIP`.

### 🖼️ Data Model

![Power BI Data Model](<images/Screenshot 2026-10-16 131245.png>)

---

## 🧮 DAX Measures & Calculated Columns

The project includes __53 measures__ organized into __14 display folders__, plus __2 calculated columns__ in `Fact_Orders`.

### 🧾 Calculated Columns

| Column | Calculation |
| --- | --- |
| order_price | Sum of item prices for the matching order_key |
| freight_price | Sum of item freight values for the matching order_key |

These columns aggregate item-level values into totals for each order.

### 📊 Main Measures

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

### ⚙️ DAX Functions Used

- `CALCULATE`
- `FILTER`
- `SUMX`
- `AVERAGEX`
- `DISTINCTCOUNT`
- `DIVIDE`
- `LOOKUPVALUE`
- `USERELATIONSHIP`
- `TREATAS`

---

## 📈 Report Snapshot

The supplied report screenshots display the following figures.

| Metric | Displayed Value |
| --- | ---: |
| Total Orders | 99.441K |
| Total Order Items | 112.650K |
| Unique Customers | 96.096K |
| Order Sales | 13.592M |
| Order Value Including Freight | 15.844M |
| Average Order Value Excluding Freight | 136.68 |
| Average Delivery Days | 12.50 |
| Total Marketing Leads | 8,000 |
| Won Leads | 842 |

---

## 🖼️ Report Screenshots

### 📊 1. Executive Overview

Summarizes order volume, sales, order value, order items, and unique customers.

The view also shows yearly trends, delivery timeliness, and sales by order status.

![Executive Overview](<images/Screenshot 2026-10-16 131300.png>)

---

### 🛍️ 2. Sales & Orders

Analyzes freight, average order value, items per order, and sales trends.

Orders are also analyzed by purchase time band and customer state.

![Sales and Orders](<images/Screenshot 2026-10-16 131317.png>)

---

### 🚚 3. Order Fulfillment

Tracks delivered and canceled orders, approval time, delivery time, and on-time delivery.

The view compares delivery performance across customer cities and shows order status trends.

![Order Fulfillment](<images/Screenshot 2026-10-16 131337.png>)

---

### 📦 4. Products & Sellers

Analyzes item sales, item prices, product counts, and seller activity.

Product categories are compared by sales and item counts. Seller locations are compared by item sales.

![Products and Sellers](<images/Screenshot 2026-10-16 131354.png>)

---

### 👥 5. Customer Analysis

Examines unique customers, repeat customers, and orders per customer.

The view compares customer cities and states by sales and order counts.

![Customer Analysis](<images/Screenshot 2026-10-16 131640.png>)

---

### 💳 6. Payments Analysis

Analyzes payment values, transaction counts, paid orders, and installments.

The view compares payment methods and displays the difference between recorded payment value and order value.

![Payments Analysis](<images/Screenshot 2026-10-16 131654.png>)

---

### 📣 7. Marketing Leads

Tracks total leads, won leads, leads without a recorded win, conversion, and average time to win.

Won leads are analyzed by business segment, business type, lead type, and win date.

![Marketing Leads](<images/Screenshot 2026-10-16 131744.png>)

---

### 🎯 8. Marketing Lead Performance

Analyzes lead origins, first-contact trends, and conversion by origin.

A matrix displays lead counts and conversion calculations across business segments and lead types.

![Marketing Lead Performance](<images/Screenshot 2026-10-16 131755.png>)

---

## 💡 Skills Demonstrated

- Data preparation and transformation with Power Query.
- Dimensional modeling with multiple fact tables.
- Surrogate key creation and relationship management.
- Integration of e-commerce and marketing data.
- DAX measures and calculated columns.
- Analysis using multiple date relationships.
- Report design across business functions.

---

## 🔗 Data Attribution

The source datasets were published by __Olist__ on Kaggle.

- [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce/data)
- [Marketing Funnel by Olist](https://www.kaggle.com/datasets/olistbr/marketing-funnel-olist)

Dataset attribution and license details are available on the linked source pages.
