# SQL-product-analytics-exercises
This folder contains hands-on exercises to practice data extraction, aggregation, filtering, and analysis using SQL. Each exercise demonstrates the ability to extract insights from datasets and simulate real business questions.
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
  
* **Price range**: Our orders range **from 50$ to 200$**, showing a good variety in the types of products customers are choosing.

Products recommendations : 
* Promote **Tires C** as a featured product.

* Investigate **early-month purchasing behavior** to see if marketing campaigns influenced sales.

* Analyze **customer segmentation** to identify high-value buyers

Dashboard :

<img width="1202" height="845" alt="Capture d’écran 2026-03-10 à 10 35 11 PM" src="https://github.com/user-attachments/assets/e23df685-d06b-44c0-ad21-910aa0472d3d" />
