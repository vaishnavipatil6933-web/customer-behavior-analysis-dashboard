# Customer Behavior Analysis

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white) ![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat&logo=postgresql&logoColor=white) ![AWS S3](https://img.shields.io/badge/AWS%20S3-569A31?style=flat&logo=amazons3&logoColor=white) ![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=flat&logo=powerbi&logoColor=black)
   
An end-to-end analytics project that turns raw, fragmented retail transaction data into an interactive Power BI dashboard, with the goal of identifying who the most valuable customers are, where profit is leaking, and where the business should focus its retention and pricing efforts.

## Table of Contents
- [Business Problem](#business-problem)
- [Dataset](#dataset)
- [Tools & Technologies](#tools--technologies)
- [Approach](#approach)
- [Key Insights](#key-insights)
- [Business Recommendations](#business-recommendations)
- [Dashboard Screenshots](#dashboard-screenshots)
- [Repository Structure](#repository-structure)
- [Limitations & Future Work](#limitations--future-work)

## Business Problem

A retail business had customer, order, and product data spread across disconnected, unstructured sources, with no single view tying customer behavior to profitability. This made it difficult to answer basic operational questions: which customers actually drive profit, which products carry healthy margins versus just high volume, and when in the year the business is most exposed to a revenue slowdown. The goal of this project was to consolidate that data into one analytical pipeline and surface the patterns the business needed to make retention, pricing, and regional decisions.

## Dataset

The dataset is a retail orders and customer practice dataset sourced from **Maven Analytics**, covering order-level transactions, customer demographics and location, and product/category details across a multi-year period (2016–2020). It is a practice dataset rather than live production data, so the workflow and analytical approach are the focus here, not the literal business figures.

## Tools & Technologies

- **Python** — data cleaning and preprocessing
- **SQL** — joining and integrating customer, order, and product tables into a unified dataset
- **AWS S3** — central storage for the cleaned dataset, used as the source Power BI connected to for visualization
- **Power BI** — interactive dashboard development and DAX-based metrics

## Approach

1. **Data cleaning (Python):** loaded the raw customer, order, and product files; removed duplicate records; handled missing values in order and customer fields; standardized data types (dates, IDs, currency fields) so tables could be joined cleanly.
2. **Data integration (SQL):** joined the orders table to customers (on customer ID) and to products (on product ID) to build a single fact table containing order details, customer attributes, and product/category attributes.
3. **Storage (AWS S3):** uploaded the cleaned, joined dataset to an S3 bucket, which served as the data source for the Power BI dashboard.
4. **Dashboard development (Power BI):** built three connected report pages — an executive overview, a customer behavior and retention view, and a product/demand view — with slicers for category, gender, city, and order date so the business can filter by segment.

## Key Insights

- The business generated **₹29.40M in profit** across **24K orders** from **11K customers**, with a **57.85% repeat customer rate** (6.58K repeat vs. 4.79K one-time customers).
- Profit is heavily concentrated among a small group of customers: the top customer alone (Matthew Flemming) contributes ₹40K, while most other top-10 customers cluster between ₹22K–29K — a small set of accounts is disproportionately responsible for profit.
- Monthly trends show a sharp performance drop in **March–April** across profit, orders, and active customers, followed by a steady recovery and a strong **year-end peak in December**.
- Product demand is relatively stable across the top-selling items (roughly 300–470 units each), but profit per product varies widely (₹0.05M–₹0.30M) — this is a margin problem, not a demand problem. The WWI Desktop PC2.33 X2330 Black drives the most profit despite comparable unit sales to lower-margin products.
- Category-level demand fell from roughly 25K units to under 5K units during the March–April dip, and category rankings shift meaningfully over the year, indicating seasonal preference changes rather than a flat demand pattern.
- Customer activity is geographically concentrated in **North America, Europe, and Australia**, and the online channel (₹5.88M) vastly outperforms any individual physical-store state, with Nevada, New Mexico, Nebraska, and Kansas each contributing a roughly even ₹0.71M–0.73M.

## Business Recommendations

- **Investigate the March–April dip** (e.g., inventory gaps, paused marketing, seasonal demand) and incorporate the pattern into demand forecasting and inventory planning so the business isn't caught off guard by a recurring seasonal slowdown.
- **Launch targeted re-engagement campaigns** for the 42% of customers who are one-time buyers, since converting even a fraction of them into repeat customers would meaningfully grow the already-strong 57.85% retention base.
- **Treat top-customer concentration as a revenue risk.** A small number of accounts driving a large share of profit is good for short-term revenue but risky long-term; consider account management or loyalty tiers for top customers while investing in acquisition to diversify the customer base.
- **Run a pricing and cost review on high-volume, low-margin products.** Since demand is stable but margins vary widely, the immediate profit lever is product-level pricing or supplier cost optimization, not driving more volume.
- **Prioritize marketing and logistics investment in North America, Europe, and Australia**, the markets where the business already has proven traction, before committing budget to untested regions.
- **Evaluate whether physical-store states should be scaled or rationalized**, given that the online channel alone outperforms all four physical states combined by a wide margin.

## Dashboard Screenshots

**Executive Business Overview** — high-level KPIs and monthly trend lines for profit, orders, and active customers.
![Executive Business Overview]("C:\Users\vcvm2\OneDrive\customer\Overview.png")

**Customer Behavior & Retention Insights** — top customers by profit contribution, repeat vs. new customer split, and geographic distribution.
![Customer Behavior & Retention Insights]("C:\Users\vcvm2\OneDrive\customer\customer behaviour insights.png")

**Product Demand vs. Profit Analysis** — quantity sold vs. profit by product, category demand trends over time, and store performance by state.
![Product Demand vs Profit Analysis]("C:\Users\vcvm2\OneDrive\customer\Product and market.png")

## Repository Structure

```
.
├── README.md
├── data/                  # raw and cleaned datasets (or .gitignore if excluded)
├── notebooks/             # Python data cleaning scripts/notebooks
├── sql/                   # SQL scripts used for joining/integration
├── dashboard/             # Power BI .pbix file
└── screenshots/           # dashboard page exports used in this README
```

## Limitations & Future Work

- The dataset is a practice dataset, not live production data, so figures reflect the analytical workflow rather than a real company's actuals.
- With more granular, transaction-level timestamps, the March–April dip could be modeled with a proper time-series forecasting approach instead of visual trend inspection.
- A churn/repeat-purchase prediction model could be built on top of the existing repeat-vs-new customer flag to proactively flag at-risk customers before they churn.
