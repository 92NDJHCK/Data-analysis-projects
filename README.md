## About This Repository 

This repository serves as a personal portfolio showcasing end-to-end Data & Web Analytics projects. It combines hands-on experience in **SQL data extraction & analysis**, **interactive BI dashboards (Power BI & Tableau)** and **automated Python ETL pipelines (API ingestion & Pandas cleaning)**, to derive actionable business insights.

# SQL Project

# Data strategy & architecture

This section describes the framework and technical structure used to ensure data quality and project viability.

## 1. The 7V framework (strategic analysis)

The project is evaluated using the 7V model to balance technical constraints with business value.
<img width="551" height="181" alt="Capture d’écran 2026-03-12 à 11 45 27 AM" src="https://github.com/user-attachments/assets/5d08c917-0f53-4fac-984a-e6356ea47aa1" />

Note : The data was already clean. I focused on preparing it for analysis and BI integration.

## 2. Data dictionary
<img width="709" height="82" alt="Capture d’écran 2026-03-12 à 12 12 13 PM" src="https://github.com/user-attachments/assets/a8aee99f-d87f-4a8f-8fa6-6437cf640ff4" />


## 3. Data schema

The following diagram represents the structure of the orders table. It identifies the unique keys and the relationships within the dataset.
<img width="396" height="187" alt="Capture d’écran 2026-03-12 à 11 55 23 AM" src="https://github.com/user-attachments/assets/f42649cc-af5d-49e9-afeb-e8dd1f0c100d" />

   
**Date formatting**: Date columns were converted to the Date type in Excel. This helps SQL and Tableau organize the data by day, month, or year.
**Data typing (BI)**: In Tableau, dimensions (IDs, product names) and measures (prices/amounts) were separated. This makes sure the calculations (like (sum) or (average)) are correct.
**Currency**: The $ (Dollar) symbol was added in Tableau to make the reports easier to read for the business.

# - Top orders
**Objective** : Analyze the initial transaction log to identify top-performing products and customer purchasing behavior for the period of January 1st–6th, 2026.

SQL query:

```sql
SELECT *

FROM orders

ORDER BY amount DESC;
```

<img width="284" height="125" alt="Exercice 1  SQL" src="https://github.com/user-attachments/assets/81d6b20b-5c45-416b-a0f6-8ea27228ce83" />

Products insights : 

* Based on the results, we can see that **the revenue Leader** is **Tires C** (Order ID: 3) is the top product in this dataset, generating $200.00 in a single transaction from customer_103.
  
* **Sales consistency**: The data shows a steady flow of one order per day. It’s interesting to note that the highest-value orders happened right at the start of the month (Jan 2nd and 3rd).
  
* **Price range**: Our orders range **from $50 to $200**, showing a good variety in the types of products customers are choosing.

Products recommendations : 
* Promote **Tires C** as a featured product.

* Investigate **early-month purchasing behavior** to see if marketing campaigns influenced sales.

* Analyze **customer segmentation** to identify high-value buyers

Dashboard :
<img width="1001" height="708" alt="Capture d’écran 2026-03-13 à 1 14 18 PM" src="https://github.com/user-attachments/assets/eefe6083-9943-4d35-a3b1-3ab41c3f7dc4" />

🚀 [View Interactive Dashboard: Tableau Public Link](https://public.tableau.com/views/Salesoperationsdashboard-Jan2026/Tableaudebord1?:language=fr-FR&publish=yes&:sid=&:display_count=n&:origin=viz_share_link)

# - Customer Insights & Performance Metrics
**Objective**: Calculate key business metrics (Revenue, AOV, Order Frequency) and filter high-value transactions to define customer segments.

## 1. Revenue per product

SQL query:

```sql
SELECT product, SUM(amount) AS revenue

FROM orders

GROUP BY product

ORDER BY revenue DESC;
```
<img width="159" height="129" alt="Capture d’écran 2026-03-12 à 4 36 02 PM" src="https://github.com/user-attachments/assets/8837bfcc-a0a9-4d57-b44a-8094e9a02e11" />

Products insights : 

* Top Performer: Tires C is the clear leader with $200.00.

* Average revenue: Tires B follows closely with $150.00.

* Lowest revenue: Tires A generates the lowest revenue ($50.00).
  

## 2. Global business metrics (total revenue, orders & AOV)
   
SQL query :

```sql
SELECT

SUM(amount) AS total_revenue,

COUNT(order_id) AS total_orders,

ROUND(AVG(amount),2) AS average_order_value

FROM orders;
```

<img width="401" height="63" alt="Capture d’écran 2026-03-12 à 4 48 34 PM" src="https://github.com/user-attachments/assets/d701a9bc-017e-45f5-8d15-734f51ef7379" />

Key Metrics:
* Total Revenue: $660.00

* Total Orders: 6

* Average order value (AOV): $110.00
  

## 3. High-value analysis (products > $150)
   
SQL query:

```sql
SELECT order_id, product, SUM(amount) AS revenue

FROM orders

GROUP BY order_id, product 

HAVING SUM(amount) > 150;
```

<img width="209" height="66" alt="Capture d’écran 2026-03-12 à 5 02 13 PM" src="https://github.com/user-attachments/assets/78fd1eb3-d524-47f9-8ad8-0f3a963d7b69" />


Insights:

* Premium concentration: Only one transaction (Order_id = 3) exceeds the $150 threshold.

* Customer profile: Customer_103 is currently the only "Premium" buyer in our dataset.

Dashboard :

<img width="993" height="786" alt="Capture d’écran 2026-03-13 à 2 13 13 PM" src="https://github.com/user-attachments/assets/5ec66a68-9408-4b59-bece-0d5e09727cc9" />


🚀[View Interactive Dashboard: Tableau Public Link](https://public.tableau.com/views/RevenueAnalyticsOrderSegmentationDashboard/Revenueanalyticsordersegmentationdashboard?:language=fr-FR&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)



# POWER BI PROJECT


# 📊 Data Professional Survey Dashboard

## Project Overview
An interactive Power BI dashboard analyzing career data, salaries, tech stacks, and job satisfaction from a global survey of data professionals.
<img width="1426" height="807" alt="Capture d’écran 2026-10-20 à 22 14 09" src="https://github.com/user-attachments/assets/32644523-6e54-411d-8fe6-4f70d604d956" />

## Key Insights
- **Demographics:** 630 survey participants with an average age of 30 years (29.87).
- **Geographic breakdown:** Top participant countries include the United States, India, Canada, and others.
- **Compensation trends:** Data Scientists and Data Engineers report the highest average salaries among survey takers, followed by Data Architects and Data Analysts.
- **Popular tech stack:** **Python** is overwhelmingly the favorite programming language across all job titles, followed by R.
- **Job Satisfaction & Entry:**
  - **Work/Life balance:** Rated at an average of **5.74 / 10**.
  - **Salary happiness:** Rated at an average of **4.27 / 10**.
  - **Difficulty to break into Data:** ≈ 42.7% found it neither easy nor difficult, while over 45% found it difficult or very difficult.

## Business Intelligence and Source
- **Business Intelligence:** Power BI (Data Modeling, DAX measures, Visualizations)
- **Data Source:** Survey dataset (CSV) from Kaggle 
