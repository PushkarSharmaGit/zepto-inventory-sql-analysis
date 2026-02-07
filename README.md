# Zepto Inventory SQL Analysis

## Overview
This project focuses on exploring and analyzing a grocery inventory dataset using SQL. The aim was to understand real product data such as prices, discounts, stock availability, and categories by writing practical SQL queries. Through this project I practiced cleaning data, grouping information, and extracting useful insights from raw inventory data.

---

## Business Problems and Solutions

### 1. Count Total Number of Products
```sql
SELECT COUNT(*) AS total_products
FROM zepto_v2;
```
**Objective:** Understand how many products are present in the inventory.

---

### 2. Product Count per Category
```sql
SELECT category, COUNT(*) AS product_count
FROM zepto_v2
GROUP BY category
ORDER BY product_count DESC;
```
**Objective:** Identify which categories contain the highest number of products.

---

### 3. Preview Sample Data
```sql
SELECT *
FROM zepto_v2
LIMIT 8;
```
**Objective:** Quickly inspect dataset structure.

---

### 4. Check Missing Important Values
```sql
SELECT *
FROM zepto_v2
WHERE name IS NULL
   OR mrp IS NULL
   OR category IS NULL;
```
**Objective:** Detect incomplete product records.

---

### 5. Identify Unique Categories
```sql
SELECT DISTINCT category
FROM zepto_v2
ORDER BY category;
```
**Objective:** List all product categories.

---

### 6. Stock Availability Distribution
```sql
SELECT outOfStock, COUNT(*) AS item_count
FROM zepto_v2
GROUP BY outOfStock;
```
**Objective:** Understand stock availability.

---

### 7. Most Expensive Products
```sql
SELECT name, mrp
FROM zepto_v2
ORDER BY mrp DESC
LIMIT 10;
```
**Objective:** Identify premium priced products.

---

### 8. Average Selling Price per Category
```sql
SELECT category,
       ROUND(AVG(discountedSellingPrice),2) AS avg_selling_price
FROM zepto_v2
GROUP BY category
ORDER BY avg_selling_price DESC;
```
**Objective:** Compare pricing trends.

---

### 9. Highest Discount Products
```sql
SELECT name, discountPercent
FROM zepto_v2
ORDER BY discountPercent DESC
LIMIT 10;
```
**Objective:** Discover best discount deals.

---

### 10. Cheapest Product per Category
```sql
SELECT category,
       MIN(discountedSellingPrice) AS cheapest_item
FROM zepto_v2
GROUP BY category;
```
**Objective:** Identify lowest priced items.

---

### 11. Price per Gram Value Analysis
```sql
SELECT name,
ROUND(discountedSellingPrice / NULLIF(weightInGms,0),3) AS price_per_gram
FROM zepto_v2
ORDER BY price_per_gram ASC
LIMIT 15;
```
**Objective:** Find best value for money products.

---

### 12. Estimate Total Stock Value per Category
```sql
SELECT category,
       SUM(discountedSellingPrice * availableQuantity) AS stock_value
FROM zepto_v2
GROUP BY category
ORDER BY stock_value DESC;
```
**Objective:** Calculate inventory value.

---

### 13. Rank Products by Price
```sql
SELECT name, mrp,
RANK() OVER (ORDER BY mrp DESC) AS price_rank
FROM zepto_v2;
```
**Objective:** Assign ranking based on price.

---

### 14. Row Number Within Each Category
```sql
SELECT category, name, mrp,
ROW_NUMBER() OVER (PARTITION BY category ORDER BY mrp DESC) AS price_position
FROM zepto_v2;
```
**Objective:** Understand product positioning.

---

### 15. Running Stock Quantity per Category
```sql
SELECT category, name, availableQuantity,
SUM(availableQuantity) OVER (PARTITION BY category ORDER BY weightInGms) AS running_quantity
FROM zepto_v2;
```
**Objective:** Track cumulative stock movement.

---

## Conclusion
This project helped me understand how SQL works with real datasets. I learned how to explore, clean, group, and analyze data using practical queries and window functions. It provided hands on experience and built a strong foundation in SQL.
