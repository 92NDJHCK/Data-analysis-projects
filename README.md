# SQL-product-analytics-exercises
This folder contains hands-on exercises to practice data extraction, aggregation, filtering, analysis using SQL and interactive dashboards created with Tableau. Each exercise demonstrates the ability to extract insights from datasets and simulate real business questions.

# 📊 Data strategy & architecture

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

# Exercice 1 - Top orders
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

🚀 [View Interactive Dashboard: Tableau Public Link][(https://public.tableau.com/shared/5KKTQGWKB?:display_count=n&:origin=viz_share_link)](https://public.tableau.com/views/Salesoperationsdashboard-Jan2026/Tableaudebord1?:language=fr-FR&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

# Exercice 2 - Customer Insights & Performance Metrics
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

<img width="1436" height="844" alt="Capture d’écran 2026-03-13 à 2 05 50 PM" src="https://github.com/user-attachments/assets/965b4d93-e135-4bad-b5cc-1afe35515556" />


[View Interactive Dashboard: Tableau Public Link](https://public.tableau.com/views/RevenueAnalyticsOrderSegmentationDashboard/Revenueanalyticsordersegmentationdashboard?:language=fr-FR&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)
