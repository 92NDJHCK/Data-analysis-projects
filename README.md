# SQL-product-analytics-exercises
This folder contains hands-on exercises to practice data extraction, aggregation, filtering, analysis using SQL and interactive dashboards created with Tableau. Each exercise demonstrates the ability to extract insights from datasets and simulate real business questions.
📊 Data Strategy & Architecture
This section describes the framework and technical structure used to ensure data quality and project viability.

1. The 7V Framework (Strategic Analysis)
The project is evaluated using the 7V model to balance technical constraints with business value.
<img width="551" height="181" alt="Capture d’écran 2026-03-12 à 11 45 27 AM" src="https://github.com/user-attachments/assets/5d08c917-0f53-4fac-984a-e6356ea47aa1" />

_Note:_ The data was already clean. I focused on preparing it for analysis an BI integration.

2. Data Dictionary
  <img width="687" height="81" alt="Capture d’écran 2026-03-12 à 11 49 29 AM" src="https://github.com/user-attachments/assets/c24e4514-17ab-424b-8a60-f2028a6af3ff" />

3. Data schema
The following diagram represents the structure of the orders table. It identifies the unique keys and the relationships within the dataset.
<img width="396" height="187" alt="Capture d’écran 2026-03-12 à 11 55 23 AM" src="https://github.com/user-attachments/assets/f42649cc-af5d-49e9-afeb-e8dd1f0c100d" />

   
**Date Formatting**: I changed the date column to the Date type in Excel. This helps SQL and Tableau organize the data by day, month, or year.
**Data Typing (BI)**: In Tableau, I separated Dimensions (IDs, Product names) from Measures (Prices/Amounts). This makes sure the calculations (like Sum or Average) are correct.
**Currency**: I added the $ (Dollar) symbol in Tableau to make the reports easier to read for the business.

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
  
* **Sales consistency**: We are seeing a steady flow of one order per day. It’s interesting to note that the highest-value orders happened right at the start of the month (Jan 2nd and 3rd).
  
* **Price range**: Our orders range **from $50 to $200**, showing a good variety in the types of products customers are choosing.

Products recommendations : 
* Promote **Tires C** as a featured product.

* Investigate **early-month purchasing behavior** to see if marketing campaigns influenced sales.

* Analyze **customer segmentation** to identify high-value buyers

Dashboard :

<img width="1202" height="845" alt="Capture d’écran 2026-03-10 à 10 35 11 PM" src="https://github.com/user-attachments/assets/e23df685-d06b-44c0-ad21-910aa0472d3d" />
📊 Interactive Dashboard https://public.tableau.com/shared/5KKTQGWKB?:display_count=n&:origin=viz_share_link

*> **Tip:** Click on the link above to open the interactive dashboard on Tableau Public. You can filter by product to explore the data.*
