# Chocolate-Sales-SQL-Project
Conducted a comprehensive SQL analysis of a chocolate retail dataset using Microsoft SQL Server Management Studio (SSMS), examining sales trends, product performance, customer purchasing patterns, and store revenue across various business dimensions.

## Table Of Content

## 📌 Project Overview

This project represents a real-world business intelligence analysis for a chocolate retail company. Using SQL, I addressed 20 business questions that required applying key database concepts, including joins, aggregate functions, subqueries, and data filtering techniques.I worked with this **Chocolate Sales Dataset** to strengthen my SQL querying skills and apply core database concepts to solve more real-world business questions.


The purpose of the analysis was to extract valuable business insights and support data-driven decision-making in areas such as:

* Revenue and profit trends
* Top-performing products, brands, and stores
* Customer segmentation by loyalty status and gender
* Geographic performance across cities and countries
  
---

## 🎯 Project Objectives

The goal of this project is to practice and demonstrate proficiency in:

* Aggregation Functions (`SUM`, `AVG`, `COUNT`)
* `GROUP BY` and `HAVING`
* Table Joins
* Subqueries
* Common Table Expressions (CTEs)
* `CASE` Statements
* Window Functions
* Data Filtering and Sorting
* Business-Oriented SQL Analysis

---

## Tools & Technologies
| TOOLS                                              | Purpose                      |
| -------------------------------------------------- | -------------------------------- |
| Microsoft SQL Server Management Studio (SSMS       | Unique identifier for each order |
| SQL Server (T-SQL)                                 | Order transaction date           |
| CSV Files                                          | Unique customer identifier       |
| GitHub | linkedln                                  | Product purchased                |



## 📊 Database Setup

Step 1 — Created a new database in SSMS:

     CREATE DATABASE ChocolateSales;

Step 2 — Imported 5 CSV files as tables using the SSMS Import Wizard:

The following tables were loaded into the database:

* sales
* products
* customers
* stores
* calendar

---

## Dataset Description

| Table            | Description                                                                                                                           |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Sales            | Transactional data including order ID,revenue,profit,quantity,discount,unit price,&foreign keys linking to customers,products,&stores |
| Product          | Product catalogue with product name, brand, category, and cocoa percentage                                                            |
| Customers        | Customer records including gender and loyalty membership status                                                                       |
| Stores           | Store details including store name, city, country, and store type                                                                     |
| Calender         | Date dimension table for time-based analysis                                                                                          |
                                                                                                                    |

## Business Questions & SQL Solutions

## Section A: Exploratory Queries (Q1–Q10)

The following queries explore each table making use of  SELECT, COUNT, SUM, MIN, MAX, DISTINCT, and WHERE to assess initial business performance metrics.

---

## Q1: How many total orders are recorded in the sales table?

    SELECT COUNT(*) AS Total_Orders
       FROM sales;

Result: 1,000,000 orders

Insight: The dataset contains 1 million transactions — a large-scale dataset reflecting a high-volume retail operation.

## Q2: List all unique product categories.

     SELECT DISTINCT category
         FROM products;

Result:

| Category   |
 -----------
| Truffle    |
 -----------
| Praline    |
 -----------
| White      |
 -----------
| Dark       |
 -----------
| Milk       | 

Insight: The business carries 5 distinct chocolate categories, offering a diverse product portfolio across premium and everyday segments.

## Q3: How many customers are registered in the dataset?

    SELECT COUNT(*) AS Total_Customers
         FROM customers;

Result: **50,000** customers

Insight: A substantial customer base of 50,000 registered users supports meaningful segmentation analysis by gender, age, and loyalty status.

## Q4: List all stores and the cities they are located in.

     SELECT
        store_name,
          city
      FROM stores;

Result (sample):

| Store Name         | City        |
 -------------------- -------------
| Chocolate Store 1  | New  York   |
 -------------------- -------------
|Chocolate Store 2   |  Melbourne  |
 -------------------- -------------
| Chocolate Store 3  |  Berlin     |
 -------------------- -------------
| Chocolate Store 4  |  Paris      |
 -------------------- -------------
| ...                | ...         |

Insight: 100 stores spread across 7 global cities, enabling geographic performance comparison across North America, Europe, and Australia.

Q5: Which products have a cocoa percentage greater than 70%?
SELECT
    product_name,
    cocoa_percent
FROM products
WHERE cocoa_percent > 70;
Result: 76 products have a cocoa percentage above 70% (at 80% or 90% cocoa levels).

Insight: Over a third of the product catalogue qualifies as premium dark/high-cocoa chocolate — a segment increasingly driven by health-conscious consumers.

Q6: How many products does each brand offer?
SELECT
    brand,
    COUNT(*) AS Product_Count
FROM products
GROUP BY brand
ORDER BY Product_Count DESC;
Result:

brand	Product_Count
Cadbury	37
Ferrero	37
Lindt	35
Mars	33
Godiva	30
Hershey	28
Insight: Cadbury and Ferrero lead portfolio size with 37 products each, while Hershey carries the smallest range. A broader portfolio often correlates with greater shelf presence and cross-sell opportunities.

Q7: Find all sales where a discount was applied.
SELECT
    order_id,
    discount
FROM sales
WHERE discount > 0;
Result: 374,872 orders included a discount — roughly 37.5% of all transactions.

Insight: More than a third of orders involved discounting, which warrants a deeper investigation into the impact on profit margins and whether discounts are driving incremental volume.

Q8: What is the total revenue generated across all sales?
SELECT
    SUM(revenue) AS Total_Revenue
FROM sales;
Result: $25,486,128.86

Insight: The business generated over $25.4 million in revenue across the two-year period — a healthy top-line figure for a multi-channel retail operation.

Q9: What is the total profit made from all orders?
SELECT
    SUM(profit) AS Total_Profit
FROM sales;
Result: $10,194,564.63

Insight: Total profit of $10.2 million represents an overall profit margin of approximately 40% — indicating strong margin management across the product catalogue.

Q10: What is the minimum and maximum profit from a single order?
SELECT
    MIN(profit) AS Minimum_Profit,
    MAX(profit) AS Maximum_Profit
FROM sales;
Result:

Minimum_Profit	Maximum_Profit
$0.73	$37.43
Insight: All orders are profitable (minimum profit > $0), suggesting no loss-making transactions exist. The wide range ($0.73 to $37.43) reflects variation in order size and discount depth.

Section B: Multi-Table Analysis — Q11 to Q20
These queries use JOIN, GROUP BY, ORDER BY, TOP, CASE WHEN, AVG, and subqueries to answer deeper cross-table analytical questions.

Q11: Total quantity sold per product category
SELECT
    p.category,
    SUM(s.quantity) AS Total_Quantity_Sold
FROM sales s
JOIN products p
    ON s.product_id = p.product_id
GROUP BY p.category
ORDER BY Total_Quantity_Sold DESC;
Result:

category	Total_Quantity_Sold
Praline	784,435
White	714,967
Dark	623,247
Truffle	462,202
Milk	385,619
Insight: Praline is the highest-volume category, outselling Milk chocolate by more than 2:1. This suggests strong consumer preference for premium filled chocolates over traditional milk variants.

## 📈 Business Questions Solved

Some of the analytical questions explored include:

1. What is the total sales revenue generated?
2. Which products generate the highest revenue?
3. Which stores perform best?
4. Who are the top customers by sales value?
5. What are the monthly sales trends?
6. Which products have the highest order volumes?
7. How do stores compare in terms of performance?
8. What are the revenue rankings across products and stores?

---

## 🔍 Key Insights

* Identified top-performing products contributing the most revenue.
* Discovered high-value customers driving sales growth.
* Analyzed store performance to determine the strongest sales locations.
* Evaluated sales trends across different periods.
* Applied ranking techniques to compare business performance metrics.

---

## 🚀 Skills Demonstrated

* SQL Query Writing
* Data Analysis
* Data Aggregation
* Relational Database Management
* Business Intelligence Thinking
* Data Storytelling through SQL

---

## 📂 Repository Structure

```text
Chocolate-Sales-SQL-Project/
│
├── Dataset/
│   ├── sales.csv
│   ├── products.csv
│   ├── customers.csv
│   ├── stores.csv
│   └── calendar.csv
│
├── SQL Queries/
│   └── chocolate_sales_queries.sql
│
├── Screenshots/
│   └── query_outputs/
│
└── README.md
```

---

## 💡 Learning Outcome

This project helped reinforce fundamental and intermediate SQL concepts while improving my ability to extract meaningful business insights from relational datasets. Through hands-on practice with joins, aggregations, subqueries, CTEs, and window functions, I gained deeper confidence in solving real-world data analysis problems using SQL.

---

## Author

**Clement Eghosa [Data Analyst]**  | Power BI |SQL | EXCEL

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://linkedin.com/in/eghosa-osalob)
[![GitHub](https://img.shields.io/badge/GitHub-View%20Profile-black?logo=github)](https://github.com/Eghosa-Dataguy)

---

### Connect With Me

If you're interested in data analytics, SQL, Power BI, Excel, or Python projects, feel free to connect with me and follow my learning journey.

⭐ If you found this project helpful, consider giving the repository a star.
