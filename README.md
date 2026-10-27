# Data analysis portfolio
## About this repository 

This repository serves as a personal portfolio showcasing end-to-end Data & Web Analytics projects. It combines hands-on experience in **SQL data extraction & analysis**, **interactive BI dashboards (Power BI & Tableau)**, and **Python** to derive actionable business insights.

- SQL Project: Orders Analysis (fundamentals)
- [Power BI dashboard (PDF)](./power_bi_dashboard.pdf)
- [Dataset (CSV)](./_Python_project_.csv)
- [Python notebook](_Python_Survey_project.ipynb)


## SQL project : order analysis (fundamentals)
> Scope note: this is a mini-dataset of 6 orders (January 1st–6th, 2026), used to practice and demonstrate SQL fundamentals (`SELECT`, `WHERE`, `GROUP BY`, aggregations) and to connect the results to a Tableau dashboard. With few rows, the figures are illustrative: they showcase technique, not business conclusions.

### Data strategy & architecture

This section describes the framework and technical structure used to ensure data quality and project viability.

### 1. The 7V framework (strategic analysis)

The project is evaluated using the 7V model to balance technical constraints with business value.
<img width="551" height="181" alt="Capture d’écran 2026-03-12 à 11 45 27 AM" src="https://github.com/user-attachments/assets/5d08c917-0f53-4fac-984a-e6356ea47aa1" />

Note : The data was already clean. I focused on preparing it for analysis and BI integration.

### 2. Data dictionary
<img width="709" height="82" alt="Capture d’écran 2026-03-12 à 12 12 13 PM" src="https://github.com/user-attachments/assets/a8aee99f-d87f-4a8f-8fa6-6437cf640ff4" />

### 3. Data schema

The following diagram represents the structure of the orders table. It identifies the unique keys and the relationships within the dataset.

<img width="396" height="187" alt="Capture d’écran 2026-03-12 à 11 55 23 AM" src="https://github.com/user-attachments/assets/f42649cc-af5d-49e9-afeb-e8dd1f0c100d" />

**Date formatting**: Date columns were converted to the Date type in Excel. This helps SQL and Tableau organize the data by day, month, or year.

**Data typing (BI)**: In Tableau, dimensions (IDs, product names) and measures (prices/amounts) were separated. This makes sure the calculations (like (sum) or (average)) are correct.

**Currency**: The $ (Dollar) symbol was added in Tableau to make the reports easier to read for the business.

### Top orders
**Objective** : Analyze the initial transaction log to identify the highest-value orders for the period of January 1st–6th, 2026.

SQL query:

```sql
SELECT *

FROM orders

ORDER BY amount DESC;
```

<img width="284" height="125" alt="Exercice 1  SQL" src="https://github.com/user-attachments/assets/81d6b20b-5c45-416b-a0f6-8ea27228ce83" />

Products insights : 

* The highest-value order is #3 (Tires C, $200.00).
  
* **Price range**: Our orders range **from $50 to $200**.

**What this exercise shows:**
* Ranking orders by value, and computing revenue per product.
* With a larger dataset, I would next look at purchase timing by day or month and at revenue per customer.

Dashboard :
<img width="1001" height="708" alt="Capture d’écran 2026-03-13 à 1 14 18 PM" src="https://github.com/user-attachments/assets/eefe6083-9943-4d35-a3b1-3ab41c3f7dc4" />

[View Interactive Dashboard: Tableau Public Link](https://public.tableau.com/views/Salesoperationsdashboard-Jan2026/Tableaudebord1?:language=fr-FR&publish=yes&:sid=&:display_count=n&:origin=viz_share_link)

### Performance Metrics
**Objective**: Calculate key business metrics (revenue, order count, AOV) and filter high-value transactions.

#### 1. Revenue per product

SQL query:

```sql
SELECT product, SUM(amount) AS revenue

FROM orders

GROUP BY product

ORDER BY revenue DESC;
```
<img width="159" height="129" alt="Capture d’écran 2026-03-12 à 4 36 02 PM" src="https://github.com/user-attachments/assets/8837bfcc-a0a9-4d57-b44a-8094e9a02e11" />

Products insights : 

The result above ranks products by total revenue. Total revenue across all products is shown in the next query ($660.00).
  

#### 2. Global business metrics (total revenue, orders & AOV)
   
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
  

#### 3. High-value analysis (order > $150)
   
SQL query:

```sql
SELECT order_id, product, SUM(amount) AS revenue

FROM orders

GROUP BY order_id, product 

HAVING SUM(amount) > 150;
```

<img width="209" height="66" alt="Capture d’écran 2026-03-12 à 5 02 13 PM" src="https://github.com/user-attachments/assets/78fd1eb3-d524-47f9-8ad8-0f3a963d7b69" />


Insights:
Only one order (#3) exceeds $150.

Dashboard :

<img width="993" height="786" alt="Capture d’écran 2026-03-13 à 2 13 13 PM" src="https://github.com/user-attachments/assets/5ec66a68-9408-4b59-bece-0d5e09727cc9" />


[View Interactive Dashboard: Tableau Public Link](https://public.tableau.com/views/RevenueAnalyticsOrderSegmentationDashboard/Revenueanalyticsordersegmentationdashboard?:language=fr-FR&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)



## POWER BI project : data professional survey

### Project overview
An interactive Power BI dashboard analyzing career data, salaries, tech stacks, and job satisfaction from a global survey of data professionals.
<img width="1426" height="807" alt="Capture d’écran 2026-10-20 à 22 14 09" src="https://github.com/user-attachments/assets/32644523-6e54-411d-8fe6-4f70d604d956" />

### Key insights
- **Demographics:** 630 survey participants with an average age of 30 years (29.87).
- **Geographic breakdown:** Top participant countries include the United States, India, Canada, and others.
- **Compensation trends:** Data Scientists and Data Engineers report the highest average salaries among survey takers, followed by Data Architects and Data Analysts.
- **Popular tech stack:** **Python** is overwhelmingly the favorite programming language across all job titles, followed by R.
- **Job Satisfaction & Entry:**
  - **Work/Life balance:** Rated at an average of **5.74 / 10**.
  - **Salary happiness:** Rated at an average of **4.27 / 10**.
  - **Difficulty to break into Data:** ≈ 42.7% found it neither easy nor difficult, while over 45% found it difficult or very difficult.

### Business intelligence and source
- **Business intelligence:** Power BI (Data Modeling, DAX measures, Visualizations)
- **Data Source:** [Dataset (CSV)](./_Python_project_.csv)
- **Power BI report:** [View the interactive report](https://app.powerbi.com/links/o5o5lzL7YH?ctid=a2697119-66c5-4126-9991-b0a8d15d367f&pbi_source=linkShare&bookmarkGuid=f9312a47-f44d-4465-9740-a04ae2b99de6)



## Python project: data professional survey EDA
### Project overview

An Exploratory Data Analysis (EDA) on the global Data Professional Survey dataset using Python to clean complex text fields, calculate salary distribution, and visualize key trends.

The use of the same database used on Power BI  but on Python with career data, salaries, tech stacks, and job satisfaction from a global survey of data professionals.

**Source notebook:**
[Notebook](_Python_Survey_project.ipynb)

Python query :

```python
import pandas as pd
import matplotlib.pyplot as plt

pd.set_option("display.max_columns", None)
df = pd.read_csv(r"_Python_project_.csv")

# Explore the dataset
df.head()       # first rows
df.shape        # number of rows and columns
df.info()       # column types and missing values
df.describe()   # basic statistics

# Drop columns not needed for this analysis
df = df.drop(columns=df.columns[4:9])

# Convert salary ranges (e.g. "100k-120k") into an estimated average salary
Salary = df["Q3 - Current Yearly Salary (in USD)"]
Salary = Salary.str.replace('+', '', regex=False)
df[['Low', 'High']] = Salary.str.split('-', expand=True)
df['Low'] = df['Low'].str.replace('k', '', regex=False).astype(float) * 1000
df['High'] = df['High'].str.replace('k', '', regex=False).astype(float) * 1000
df["Q3 - Current Yearly Salary (in USD)"] = (df['Low'] + df['High']) / 2
df = df.drop(columns=['Low', 'High'])

# Check missing values after the conversion
print(df["Q3 - Current Yearly Salary (in USD)"].isna().sum())

# Group all "Other..." answers into a single "Other" category
masque = df["Q1 - Which Title Best Fits your Current Role?"].str.startswith("Other", na=False)
df.loc[masque, "Q1 - Which Title Best Fits your Current Role?"] = "Other"

masque = df["Q4 - What Industry do you work in?"].str.startswith("Other", na=False)
df.loc[masque, "Q4 - What Industry do you work in?"] = "Other"

masque = df["Q11 - Which Country do you live in?"].str.startswith("Other", na=False)
df.loc[masque, "Q11 - Which Country do you live in?"] = "Other"

masque = df["Q5 - Favorite Programming Language"].str.startswith("Other", na=False)
df.loc[masque, "Q5 - Favorite Programming Language"] = "Other"
``` 

Full code with all charts: [Python notebook](_Python_Survey_project.ipynb)


### Key steps & highlights
- **Data cleaning & parsing:** Converted textual salary ranges (e.g., `100k-120k`) into numeric bounds to compute estimated average yearly compensation.
- **Handling missing values:** Performed strict NaN validation to ensure data integrity during text-to-float transformations.
- **Category standardization:** Cleaned and grouped multi-variant responses (such as "Other...") across roles, industries, countries, and languages.
- **Exploratory visualizations:** Generated plots covering:
  - Average salary distribution (Histogram) : 
  - Top favorite programming languages (Horizontal bar chart)
  - Job satisfaction across 6 Key Pillars (Bar chart)
  - Top working industries (Horizontal bar chart)
  - Relationship between age and compensation (Scatter plot)
    
### Visualizations & key insights

<img width="606" height="451" alt="Capture d’écran 2026-10-23 à 14 30 50" src="https://github.com/user-attachments/assets/e795a763-6402-47f2-ac5b-13453efbb8ab" />

**Distribution of average salary in USD:** The salary distribution is right-skewed. The vast majority of respondents earn within the lower brackets (under $50,000), with a sharp peak around $25,000. Higher salary brackets ($100,000+) contain significantly fewer respondents, pulling up the overall average.

<img width="729" height="439" alt="Capture d’écran 2026-10-23 à 14 31 10" src="https://github.com/user-attachments/assets/72c22149-2323-4ef9-a5dd-f31db282bae1" />

**Favorite programming language:** Python is overwhelmingly the dominant language chosen by data professionals, with over 400 respondents. It is followed distantly by R and the "Other" category, while Java, JavaScript, and C/C++ register very low adoption in this specific dataset.   

<img width="1150" height="437" alt="Capture d’écran 2026-10-23 à 14 31 22" src="https://github.com/user-attachments/assets/2680e0ce-1786-439c-b7cb-7e2c901021fb" />

**Job satisfaction:** Respondents report the highest satisfaction levels in coworkers and Work/Life balance (both scoring close to 5.8 / 10).
Conversely, salary satisfaction receives the lowest score (around 4.2 / 10), indicating a widespread desire for better financial compensation across roles.

<img width="742" height="428" alt="Capture d’écran 2026-10-23 à 14 32 33" src="https://github.com/user-attachments/assets/cfdb23a8-058b-4849-9d49-5da401d161fb" />

**Top industries:** Aside from the grouped "Other" category, Tech is by far the leading industry employing data professionals (around 150 respondents), followed by Finance and Healthcare. Traditional sectors like Real Estate, Construction, and Agriculture show much lower representation.

<img width="872" height="480" alt="Capture d’écran 2026-10-23 à 14 32 47" src="https://github.com/user-attachments/assets/7e7b08c0-907f-44a4-b7e0-ae9c92d59b36" />

**Relationship Between Age and Salary:** The scatter plot reveals that high earners ($125,000 to nearly $200,000) are primarily concentrated within the core working age bracket of 25 to 45 years old. Extreme age groups (under 20 or over 60) mostly cluster around entry-level or lower salary tiers.

### Limitations
- **Salaries are estimates.** The survey gives salary ranges (e.g. `100k-120k`), so I used the midpoint of each range. This smooths the real distribution and can create artificial peaks in the histogram.
- **Open-ended ranges and missing values.** Ranges without an upper bound (e.g. `200k+`) and non-numeric answers end up as NaN and are excluded from salary averages. 2 respondents are affected.
- **Self-selected sample.** 630 respondents who chose to answer a survey, so the results are not representative of all data professionals.
- **Self-reported data.** Salaries and satisfaction scores are declared, not verified.
- **Columns dropped by position.** Columns 4 to 8 were removed because they were not needed for this analysis.
- **The age/salary scatter plot is descriptive only:** no correlation or statistical test was computed.

