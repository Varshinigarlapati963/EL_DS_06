# EL_DS_06
# Online Sales Data Analysis using MariaDB
This project focuses on performing SQL-based data analysis on a sample online_sales_data dataset using MariaDB. The objective is to extract insights such as top-performing product categories, regional sales trends, and monthly performance across different markets.

## Dataset Overview
Table: online_sales_data
Columns:
Transaction ID: Unique identifier for each transaction
Date: Date of the transaction
Product Category: Category of the product sold
Product Name: Name of the product
Units Sold: Number of units sold
Unit Price: Price per unit
Total Revenue: Calculated as Units Sold × Unit Price
Region: Sales region (e.g., North America, Europe, Asia)
Payment Method: Mode of payment used
SQL Queries and Insights
## 1. Top Product Category in Q1
  ```python 
   SELECT
  `Product Category`,
 ROUND(SUM(`Total Revenue`), 2) AS total_revenue
  FROM online_sales_data
WHERE MONTH(`Date`) IN (1, 2, 3)
GROUP BY `Product Category`
ORDER BY total_revenue DESC
LIMIT 1;
```
Insight: The Electronics category generated the highest revenue in Q1, totaling 15,399.68.


## 2.Top Product Category Overall
```python
SELECT
  `Product Category`,
  ROUND(SUM(`Total Revenue`), 2) AS total_revenue
FROM online_sales_data
GROUP BY `Product Category`
ORDER BY total_revenue DESC
LIMIT 1;
```
Insight: The Electronics category is the overall top performer with 34,982.41 in revenue.

## 3.Monthly Sales by Region
```python
SELECT
  Region,
  YEAR(Date) AS order_year,
  MONTH(Date) AS order_month,
  SUM(`Total Revenue`) AS total_revenue,
  COUNT(DISTINCT `Transaction ID`) AS total_orders
FROM online_sales_data
GROUP BY Region, YEAR(Date), MONTH(Date)
ORDER BY Region, order_year, order_month;
```
Insight: Revenue and order trends are broken down by region and month. This allows identifying seasonal trends and regional performance.

## 4.Overall Monthly Performance
```python
SELECT
  YEAR(Date) AS order_year,
  MONTH(Date) AS order_month,
  SUM(`Total Revenue`) AS total_revenue,
  COUNT(DISTINCT `Transaction ID`) AS total_orders
FROM online_sales_data
GROUP BY YEAR(Date), MONTH(Date)
ORDER BY order_year, order_month;
```
Insight: This query shows how total revenue and order volume change each month, useful for identifying peak sales periods.


