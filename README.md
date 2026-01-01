# Business Problem Statement

A leading retail company wants to better understand its customers' shopping behavior in order to improve sales, customer satisfaction, and long-term loyalty. The management team has noticed changes in purchasing patterns across demographics, product categories, and sales channels (online vs. offline). They are particularly interested in uncovering which factors, such as discounts, reviews, seasons, or payment preferences, drive consumer decisions and repeat purchases.

You are tasked with analyzing the company's consumer behavior dataset to answer the following overarching business question:

* How can the company leverage consumer shopping data to identify trends, improve customer engagement, and optimize marketing and product strategies?

### Deliverables

1. Data Preparation & Modeling (Python): Clean and transform the raw dataset for analysis.

2. Data Analysis (SQL): Organize the data into a structured format, simulate business transactions, and run queries to extract insights on customer segments, loyalty, and purchase drivers.

3. Visualization & Insights (Power BI): Build an interactive dashboard that highlights key patterns and trends, enabling stakeholders to make data-driven decisions.

4. GitHub Repository: Include all Python scripts, SQL queries, and dashboard files in a well-structured repository.



# Project Overview

This project analyzes customer shopping behavior using transactional data from 3,900 purchases across various product categories. The goal is to uncover insights into spending patterns, customer segments, product preferences, and subscription behavior to guide strategic business decisions.

### Dataset Summary

* Rows: 3,900

* Columns: 18

### Key Features

Customer demographics (Age, Gender, Location, Subscription Status)

Purchase details (Item Purchased, Category, Purchase Amount, Season, Size, Color)

Shopping behavior (Discount Applied, Promo Code Used, Previous Purchases, Frequency of

Purchases , Review Rating, Shipping Type)

Missing Data: 37 values in Review Rating column

### Exploratory Data Analysis using Python

We began with data preparation and cleaning in Python:.

* Data Loading: Imported the dataset using pandas.
```python
# Loading the dataset using pandas
import pandas as pd
df = pd.read_csv(r"C:\Users\user\Documents\End_to_BI_Solution.csv")
```

* Initial Exploration: Used of info) to check structure and describe() for summary statistics.

```python
# Summary statistics using .describe()
df.describe(include='all')
```

## 📊 Dataset Summary (Customer Shopping Behavior)

| Statistic | Customer ID | Age | Gender | Item Purchased | Category | Purchase Amount (USD) | Location | Size | Color | Season | Review Rating | Subscription Status | Shipping Type | Discount Applied | Promo Code Used | Previous Purchases | Payment Method | Frequency of Purchases |
|----------|-------------|-----|--------|----------------|----------|----------------------|----------|------|-------|--------|---------------|---------------------|--------------|------------------|-----------------|--------------------|---------------|----------------------|
| Count | 3900 | 3900 | 3900 | 3900 | 3900 | 3900 | 3900 | 3900 | 3900 | 3900 | 3863 | 3900 | 3900 | 3900 | 3900 | 3900 | 3900 |
| Unique | NaN | NaN | 2 | 25 | 4 | NaN | 50 | 4 | 25 | 4 | NaN | 2 | 6 | 2 | 2 | NaN | 6 | 7 |
| Top | NaN | NaN | Male | Blouse | Clothing | NaN | Montana | M | Olive | Spring | NaN | No | Free Shipping | No | No | NaN | PayPal | Every 3 Months |
| Frequency | NaN | NaN | 2652 | 171 | 1737 | NaN | 96 | 1755 | 177 | 999 | NaN | 2847 | 675 | 2223 | 2223 | NaN | 677 | 584 |
| Mean | 1950.5 | 44.068 | NaN | NaN | NaN | 59.764 | NaN | NaN | NaN | NaN | 3.750 | NaN | NaN | NaN | NaN | 25.352 | NaN | NaN |
| Std | 1125.98 | 15.208 | NaN | NaN | NaN | 23.685 | NaN | NaN | NaN | NaN | 0.717 | NaN | NaN | NaN | NaN | 14.447 | NaN | NaN |
| Min | 1 | 18 | NaN | NaN | NaN | 20 | NaN | NaN | NaN | NaN | 2.5 | NaN | NaN | NaN | NaN | 1 | NaN | NaN |
| 25% | 975.75 | 31 | NaN | NaN | NaN | 39 | NaN | NaN | NaN | NaN | 3.1 | NaN | NaN | NaN | NaN | 13 | NaN | NaN |
| 50% | 1950.5 | 44 | NaN | NaN | NaN | 60 | NaN | NaN | NaN | NaN | 3.8 | NaN | NaN | NaN | NaN | 25 | NaN | NaN |
| 75% | 2925.25 | 57 | NaN | NaN | NaN | 81 | NaN | NaN | NaN | NaN | 4.4 | NaN | NaN | NaN | NaN | 38 | NaN | NaN |
| Max | 3900 | 70 | NaN | NaN | NaN | 100 | NaN | NaN | NaN | NaN | 5.0 | NaN | NaN | NaN | NaN | 50 | NaN | NaN |

* Checking For Missing Valess 
```python
# Checking if missing data or null values are present in the dataset
df.isnull().sum()
```

|                      |       |
-----------------------|--------
|customer ID           |     0 |
|Age                   |     0 |
|Gender                |     0 |
|Item Purchased        |     0 |
|Category              |     0 |
|Purchase Amount (USD) |     0 |
|Location              |     0 |
|Size                  |     0 |
|Color                 |     0 |
|Season                |     0 |
|Review Rating         |    37 |
|Subscription Status   |     0 |
|Shipping Type         |     0 |
|Discount Applied      |     0 |
|Promo Code Used       |     0 |
|Previous Purchases    |     0 |
|Payment Method        |     0 |
|Frequency of Purchases|     0 |

This Output tell us that the there is 37 missing values in the column of 'Review Rating'

* Missing Data Handling: Checked for null values and imputed missing values in the Review Rating column using the median rating of each product category.
```python
# Imputing missing values in Review Rating column with the median rating of the product category
df['Review Rating'] = df.groupby('Category')['Review Rating'].transform(lambda x: x.fillna(x.median()))
```
|                      |       |
-----------------------|--------
|customer ID           |     0 |
|Age                   |     0 |
|Gender                |     0 |
|Item Purchased        |     0 |
|Category              |     0 |
|Purchase Amount (USD) |     0 |
|Location              |     0 |
|Size                  |     0 |
|Color                 |     0 |
|Season                |     0 |
|Review Rating         |     0 |
|Subscription Status   |     0 |
|Shipping Type         |     0 |
|Discount Applied      |     0 |
|Promo Code Used       |     0 |
|Previous Purchases    |     0 |
|Payment Method        |     0 |
|Frequency of Purchases|     0 |


* Column Standardization: Renamed columns to snake case for better readability and documentation

```python
#Renaming columns according to snake casing for better readability and documentation
df.columns = df.columns.str.lower()
df.columns = df.columns.str.replace(' ','_')
df = df.rename(columns={'purchase_amount_(usd)':'purchase_amount'})
```

* We add labels to each age group to better unnderstand customers based on their age.  

```python
# create a new column age_group
labels = ['Young Adult', 'Adult', 'Middle-aged', 'Senior']
df['age_group'] = pd.qcut(df['age'], q=4, labels = labels)
```


| age | age_group     |
|-----|---------------|
| 55  | Middle-aged   |
| 19  | Young Adult   |
| 50  | Middle-aged   |
| 21  | Young Adult   |
| 45  | Middle-aged   |
| 46  | Middle-aged   |
| 63  | Senior        |
| 27  | Young Adult   |
| 26  | Young Adult   |
| 57  | Middle-aged   |


* We categories purchase based on how a customer often buyers product.


```python
# create new column purchase_frequency_days
frequency_mapping = {
    'Fortnightly': 14,
    'Weekly': 7,
    'Monthly': 30,
    'Quarterly': 90,
    'Bi-Weekly': 14,
    'Annually': 365,
    'Every 3 Months': 90
}
df['purchase_frequency_days'] = df['frequency_of_purchases'].map(frequency_mapping)
```

| purchase_frequency_days | frequency_of_purchases |
|-------------------------|------------------------|
| 14                      | Fortnightly            |
| 14                      | Fortnightly            |
| 7                       | Weekly                 |
| 7                       | Weekly                 |
| 365                     | Annually               |
| 7                       | Weekly                 |
| 90                      | Quarterly              |
| 7                       | Weekly                 |
| 365                     | Annually               |
| 90                      | Quarterly              |


* Then i install SQL Alchemy (A libray that allow to transfer data for from pyhon to SQL Database such PostgreSQL etc )
```python
!pip install psycopg2-binary sqlalchemy
```

 * And then i load the data to my database

```python
from sqlalchemy import create_engine
import pandas as pd


# Step 1: Connect to PostgreSQL
username = "postgres"
password = "admin"
host = "localhost"
port = "5432"
database = "customer_shopping"

engine = create_engine(f"postgresql+psycopg2://{username}:{password}@{host}:{port}/{database}")

# Step 2: Define the Table Name

table_name = 'customer_data'

# Step 3: select columns 
columns_to_keep = [
    'customer_id',
    'age',
    'gender',
    'item_purchased',
    'category',
    'purchase_amount',
    'location',
    'size',
    'color',
    'season',
    'review_rating',
    'subscription_status',
    'shipping_type',
    'discount_applied',
    'previous_purchases',
    'payment_method',
    'frequency_of_purchases',
    'age_group',
    'purchase_frequency_days'
]

# Check if 'df' exists (for safety when running this script)
if 'df' in locals() or 'df' in globals():
    # Filter the dataframe to only include the columns listed above
    
    try:
        final_df = df[columns_to_keep]
    except KeyError as e:
        print(f"Warning: Some columns in the list were not found in the DataFrame: {e}")
        print("Uploading the full DataFrame instead.")
        final_df = df

    # Step 4: Load DataFrame into PostgreSQL
    final_df.to_sql(table_name, engine, if_exists="replace", index=False)
    print(f"Data successfully loaded into table '{table_name}' in database '{database}'.")
```


## Below Are Analysis Done in SQl Using The Data That Has Been Load From Python 


### Q1. Total revenue generated by male vs female customers
```sql
SELECT gender, SUM(purchase_amount) AS revenue
FROM customer_data
GROUP BY gender;
```

| gender | revenue |
|--------|---------|
| Male   | 157890  |
| Female | 75191   |


 ### Q2. Customers who used discounts but spent more than the average purchase amount
```sql
SELECT customer_id, purchase_amount
FROM customer_data
WHERE discount_applied = 'Yes'
AND purchase_amount >
(SELECT AVG(purchase_amount) FROM customer_data)
LIMIT 10;
```

| customer_id | purchase_amount |
|-------------|-----------------|
| 2           | 64              |
| 3           | 73              |
| 4           | 90              |
| 7           | 85              |
| 9           | 97              |
| 12          | 68              |
| 13          | 72              |
| 16          | 81              |
| 20          | 90              |
| 22          | 62              |


  
### Q3. Top 5 products with the highest average review rating
```sql   
SELECT item_purchased,
ROUND(AVG(review_rating::numeric), 2) AS average_product_rating
FROM customer_data
GROUP BY item_purchased
ORDER BY average_product_rating DESC
LIMIT 5;
```

| item_purchased | average_product_rating |
|----------------|------------------------|
| Gloves         | 3.86                   |
| Hat            | 3.80                   |
| Jacket         | 3.76                   |
| Sneakers       | 3.76                   |
| Shirt          | 3.62                   |



### Q4. Average purchase amount by shipping type

```sql  
SELECT shipping_type,
ROUND(AVG(purchase_amount), 2) AS avg_purchase
FROM customer_data
WHERE shipping_type IN ('Standard', 'Express')
GROUP BY shipping_type;
```

| shipping_type | avg_purchase |
|---------------|--------------|
| Express       | 60.48        |
| Standard      | 58.46        |



 ### Q5. Do subscribed customers spend more?
```sql  
SELECT subscription_status,
COUNT(customer_id) AS total_customers,
ROUND(AVG(purchase_amount), 2) AS avg_spend,
ROUND(SUM(purchase_amount), 2) AS total_revenue
FROM customer_data
GROUP BY subscription_status
ORDER BY total_revenue DESC;
```

| subscription_status | total_customers | avg_spend | total_revenue |
|---------------------|-----------------|-----------|---------------|
| No                  | 2847            | 59.87     | 170436.00     |
| Yes                 | 1053            | 59.49     | 62645.00      |



### Q6. Top 5 products with the highest discount rate
```sql
SELECT item_purchased,
ROUND(100.0 * SUM(CASE WHEN discount_applied = 'Yes' THEN 1 ELSE 0 END)
/ COUNT(*), 2
) AS discount_rate
FROM customer_data
GROUP BY item_purchased
ORDER BY discount_rate DESC
LIMIT 5;
```

| item_purchased | discount_rate (%) |
|----------------|-------------------|
| Hat            | 50.00             |
| Sneakers       | 49.66             |
| Coat           | 49.07             |
| Sweater        | 48.17             |
| Pants          | 47.37             |


### Q7. Customer segmentation: New, Returning, Loyal
 
```sql
WITH customer_type AS (
SELECT customer_id,
CASE WHEN previous_purchases <= 1 THEN 'New'
WHEN previous_purchases BETWEEN 2 AND 10 THEN 'Returning'
 ELSE 'Loyal'
END AS customer_segment
FROM customer_data)
SELECT customer_segment,
COUNT(*) AS number_of_customers
FROM customer_type
GROUP BY customer_segment;
```

| customer_segment | number_of_customers |
|------------------|---------------------|
| Loyal            | 3116                |
| Returning        | 701                 |
| New              | 83                  |



### Q8. Top 3 most purchased products per category
```sql 
WITH item_counts AS (
SELECT category,
item_purchased,
COUNT(*) AS total_orders,
ROW_NUMBER() OVER (
PARTITION BY category
ORDER BY COUNT(*) DESC
) AS item_rank
FROM customer_data
 GROUP BY category, item_purchased)
SELECT category, item_purchased, total_orders
FROM item_counts
WHERE item_rank <= 3;
```

| category    | item_purchased | total_orders |
|-------------|----------------|--------------|
| Accessories | Jewelry        | 171          |
| Accessories | Sunglasses     | 161          |
| Accessories | Belt           | 161          |
| Clothing    | Blouse         | 171          |
| Clothing    | Pants          | 171          |
| Clothing    | Shirt          | 169          |
| Footwear    | Sandals        | 160          |
| Footwear    | Shoes          | 150          |
| Footwear    | Sneakers       | 145          |
| Outerwear   | Jacket         | 163          |


### Q9. Repeat buyers (previous purchases > 5) by subscription
```sql
SELECT subscription_status,
COUNT(customer_id) AS repeat_buyers
FROM customer_data
WHERE previous_purchases > 5
GROUP BY subscription_status;
```

| subscription_status | repeat_buyers |
|---------------------|---------------|
| No                  | 2518          |
| Yes                 | 958           |



### Q10. Revenue contribution by age group
```sql
SELECT age_group,
SUM(purchase_amount) AS total_revenue
FROM customer_data
GROUP BY age_group
ORDER BY total_revenue DESC;
```

| age_group    | total_revenue |
|--------------|---------------|
| Young Adult  | 62143         |
| Middle-aged  | 59197         |
| Adult        | 55978         |
| Senior       | 55763         |

## And Finally I Connect My Database To Powwer BI To Build Dashboard

<img width="1310" height="666" alt="Screenshot 2025-12-31 111738" src="https://github.com/user-attachments/assets/d44a3199-b9ec-4fd5-bb3a-4023d404a08a" />


## 🧮 DAX Measures & Calculations

To drive the visualizations in this dashboard, the following DAX measures were created to aggregate the raw customer data:

| Metric | DAX Formula | Description |
| :--- | :--- | :--- |
| **Total Customers** | `Number of customer = COUNT('public customer_data'[customer_id])` | Calculates the total count of unique customer IDs. |
| **Average Purchase** | `Average Purchse Amount = AVERAGE('public customer_data'[purchase_amount])` | Calculates the mean value of all transactions. |
| **Average Rating** | `Average Review Rating = AVERAGE('public customer_data'[review_rating])` | Calculates the mean satisfaction score across all reviews. |

### Measures Snippet
```dax
// Total Number of Customers
Number of customer = COUNT('public customer_data'[customer_id])

// Average Purchase Value
Average Purchse Amount = AVERAGE('public customer_data'[purchase_amount])

// Average Customer Satisfaction
Average Review Rating = AVERAGE('public customer_data'[review_rating])
```
# Customer Behavior Analysis: Key Insights & Recommendations

## 📊 Business Insights

Based on the dashboard analysis of **3.9K customers**, the following key trends have been identified:

* **Subscription Retention Gap:** Currently, only **27% of customers are subscribers** (73% non-subscribers). This indicates a significant opportunity to convert casual shoppers into recurring members to stabilize revenue.
* **Apparel Dominance:** **Clothing** is the clear market leader in sales volume, significantly outperforming Accessories, Footwear, and Outerwear. It serves as the primary "hook" for the brand.
* **High-Value Demographic:** The **Young Adult** age group is the most profitable segment, leading in both total sales volume and revenue generation.
* **Broad Market Appeal:** Despite Young Adults leading, revenue is remarkably consistent across **Middle-aged, Senior, and Adult** groups (all near the 1,000 mark), suggesting the brand has a strong "ageless" appeal.
* **Underperforming Categories:** **Outerwear** shows the lowest sales volume, suggesting a need for seasonal promotions or a review of the current product-market fit for that category.

---

## 📈 Key Performance Indicators (KPIs)

| Metric | Value |
| :--- | :--- |
| **Total Customers** | 3.9K |
| **Average Purchase Amount** | $59.76 |
| **Average Review Rating** | 3.75 / 5.0 |

---

## 💡 Strategic Recommendations

### 1. Increase Subscription Conversion
**Action:** Implement a "Subscriber-Only" incentive, such as a 15% discount on the first order or exclusive early access to new Clothing drops.
**Objective:** Target a 10% increase in the subscription rate to drive predictable, recurring revenue.

### 2. Maximize Average Order Value (AOV)
**Action:** Since **Clothing** is the top seller, introduce "Complete the Look" bundles. Cross-sell lower-performing categories like **Accessories** or **Footwear** at the checkout page.
**Objective:** Lift the Average Purchase Amount from **$59.76** to over **$65.00**.

### 3. Demographic-Specific Marketing
**Action:** Allocate a higher percentage of the ad spend toward **Young Adult** channels (TikTok, Instagram, and Influencer partnerships).
**Objective:** Double down on the highest-performing segment to maximize ROI.

### 4. Reputation Management & Quality Control
**Action:** The current rating of **3.75** suggests some friction. Initiate a post-purchase survey program to identify specific pain points in the customer experience or product quality.
**Objective:** Improve the brand's social proof by pushing the Average Review Rating toward **4.0**.

### 5. Inventory Optimization for Outerwear
**Action:** Run a seasonal "Flash Sale" for **Outerwear** to move stagnant inventory and free up budget for high-demand Clothing items.
**Objective:** Increase stock turnover and improve category-specific sales performance.
