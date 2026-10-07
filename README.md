UrbanCart Logistics Analytics Project

A 4-week, end-to-end logistics data analytics project: strategic planning → data cleaning → exploratory analysis → predictive modeling and optimization, built around a simulated e-commerce logistics dataset ("UrbanCart").

Overview

UrbanCart is a hypothetical mid-sized e-commerce retailer operating three regional warehouses, facing late deliveries and inventory imbalances. This project simulates the full analytics lifecycle a data science team would follow to diagnose and address those problems, using a realistic simulated dataset of 50,000 orders across 2025.

Week	Focus	Report
1	Strategic Planning & Data Exploration	Week1_Strategic_Planning_Logistics_Report.docx
2	Data Collection, Cleaning & Preprocessing	Week2_Data_Collection_Cleaning_Preprocessing_Report.docx
3	Advanced Data Analysis & Visualization	Week3_Advanced_Data_Analysis_Visualization_Report.docx
4	Predictive Modeling & Optimization	Week4_Predictive_Modeling_Optimization_Report.docx
Dataset
urbancart_orders_raw.csv — 50,250 simulated orders with injected data-quality issues (missing values, outliers, duplicates, inconsistent formatting)
urbancart_orders_clean.csv — 50,000-row cleaned dataset used for Weeks 3–4 (orders, warehouses, regions, delivery partners, costs, delivery performance, Jan–Dec 2025)

Key fields: order_id, order_date, promised_date, delivery_date, warehouse_id, region, delivery_partner, sku, category, quantity, unit_cost, delivery_distance_km, package_weight_kg, delivery_time_days, delay_days, on_time, transport_cost, stock_on_hand, stockout_flag

Week 1 — Strategic Planning

Defines the UrbanCart scenario (inventory management, route optimization, supply chain integration) and three core KPIs: On-Time Delivery Rate, Inventory Turnover Ratio, and Cost per Delivery. Outlines a 5-stage analytics roadmap and maps regression, clustering, and optimization techniques to specific business questions.

Week 2 — Data Cleaning & Preprocessing

Runs an actual pandas/scikit-learn cleaning pipeline against the raw 50,250-row dataset:

4.00% of orders had a missing delivery_date → flagged (is_delivered), not dropped
3,546 rows (7.10%) flagged as statistical outliers via IQR, but only 40 rows (genuine >500km data-entry errors) removed
250 duplicate order records removed
261 raw SKU string variants standardized down to 72 true products
Min-Max and Z-score normalization applied and verified
Week 3 — Exploratory Analysis & Visualization

EDA and six visualizations (histogram/boxplot, bar charts, trend line, scatter, correlation heatmap) on the cleaned dataset. Key findings:

WH-02 handles the most orders (40.1%) but has the lowest on-time rate (68.4% vs. 84–88% at the other warehouses)
On-time rate drops from 85.3% → 61.6% during the Nov–Dec peak season
Transport cost correlates with delivery distance at r = 0.98
Rural deliveries cost 6.1× more than Urban Core on average
Week 4 — Predictive Modeling & Optimization

Two validated models trained on an 80/20 split with 5-fold cross-validation and GridSearchCV tuning:

Model	Target	Best Result
Linear Regression	delivery_time_days	R² = 0.7377, RMSE = 0.5996
Random Forest (tuned)	delivery_time_days	R² = 0.7365, RMSE = 0.6009
Logistic Regression	on_time	Accuracy = 0.8156, F1 = 0.8929
Random Forest (tuned)	on_time	Accuracy = 0.8134, F1 = 0.8920

Feature importance from the classification model confirms, with model evidence, that peak season and warehouse WH-02 — not distance — are the strongest independent predictors of late delivery, directly supporting the optimization recommendations (targeted WH-02 capacity review, seasonal resourcing ahead of November, and a precision-aware buffer for customer-facing ETA predictions).

Tech Stack

Python, pandas, numpy, scikit-learn, matplotlib, seaborn
