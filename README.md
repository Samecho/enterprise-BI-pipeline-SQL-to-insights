# enterprise-BI-pipeline-SQL-to-insights: Bike-Share Revenue & Pricing Strategy

## Executive Summary

This project delivers an end-to-end commercial analytics solution for **Toman Bike Share**, a simulated urban mobility provider. The objective was to architect a robust data pipeline—from raw SQL-based ETL to an interactive Power BI executive dashboard—to analyze key performance indicators (KPIs) and provide data-driven recommendations for a 2026 pricing strategy.

## 🏗️ Technical Architecture

The project follows a professional report development lifecycle:

1. **Data Engineering (SQL):** Multi-year dataset integration, data cleansing, and transformation.
2. **Semantic Modeling (Power BI):** Development of a Star Schema and complex DAX measures.
3. **Data Visualization:** High-fidelity UI design focusing on commercial metrics (Revenue, Profitability, Seasonal Trends).
4. **Strategic Advisory:** Price sensitivity analysis and forecasting for the upcoming fiscal year.

---

## 💻 Technical Implementation

### 1. SQL Engineering (ETL & Data Integrity)

To ensure high data quality (a key requirement for the Emera Energy role), I utilized **Common Table Expressions (CTEs)** and advanced **Joins** to merge disparate datasets.

* **Performance Optimization:** Aggregated hourly data at the source level to reduce Power BI refresh latency.
* **Data Quality Assurance:** Implemented logic to handle NULL values and ensure price-cost consistency across 2021 and 2022 records.

```sql
-- Sample logic used for the data pipeline
WITH bike_data AS (
    SELECT * FROM bike_share_yr_0
    UNION ALL
    SELECT * FROM bike_share_yr_1
)
SELECT 
    dbt.*, 
    ct.cost, 
    ct.price,
    (riders * price) AS revenue,
    (riders * price - cost * riders) AS profit
FROM bike_data dbt
LEFT JOIN cost_table ct ON dbt.yr = ct.yr;

```

### 2. Power BI & DAX Modeling

The dashboard was built using a **Star Schema** to ensure scalability and ease of use for end-users.

* **Advanced DAX:** Developed measures utilizing `CALCULATE`, `SUMX`, and `FILTER` to track dynamic performance metrics.
* **Time Intelligence:** Engineered Year-over-Year (YoY) comparisons to identify peak demand seasons.
* **Interactive Design:** Implemented slicers for "Rider Type" (Casual vs. Registered) to analyze price sensitivity across different segments.

### 3. Automation & Efficiency

* **Report Management:** Configured conditional formatting and automated alerts to highlight underperforming time slots.
* **Scalability:** Designed the ETL process to automatically incorporate new annual CSV files with minimal script adjustments.

---

## 📊 Commercial Insights & Recommendations

The analysis identified a significant revenue growth opportunity. Based on the data, the following strategy was proposed to the executive team:

* **Proposed Pricing Adjustment:** A conservative **10-15% price increase** (moving from $4.99 to approx. $5.49–$5.74).
* **Rationale:** The 2022 data showed strong demand inelasticity despite previous increases. A segmented strategy targeting "Casual" riders (who show lower price sensitivity) could maximize profit margins without sacrificing "Registered" user retention.
* **Risk Mitigation:** Recommended a "Monitor and Adjust" phase for Q1 2026 to track market response using real-time Power BI subscriptions.

---

## 📂 Project Structure

* **/SQL:** Production-ready scripts for database initialization and view creation.
* **/Power_BI:** The `.pbix` file containing the semantic model and interactive dashboard.
* **/Data:** Cleaned CSV datasets used as the source of truth.
* **/Documentation:** High-level summary of the use case and business requirements.

## 🚀 How to Run

1. **Database:** Import the CSV files in `/Data` into your SQL Server instance.
2. **ETL:** Execute the `SQL/SQL Query.txt` script to generate the consolidated view.
3. **Reporting:** Open `Power BI/Project Portfolio 1.pbix` and update the data source settings to point to your local SQL instance.

---

### Why this project matches the Emera Energy JD:

* **Commercial Focus:** Focuses on Revenue, Profit, and Pricing (Trading/Risk mindset).
* **Full Lifecycle:** Covers everything from requirement gathering to deployment.
* **Advanced Tools:** Demonstrates proficiency in SQL, DAX, and professional Report Design.
* **QA Mindset:** Explicitly mentions data integrity and validation checks.
