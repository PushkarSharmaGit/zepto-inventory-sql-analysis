# Zepto Inventory SQL Analysis

## Overview
This project focuses on exploring and analyzing a grocery inventory dataset using SQL. The aim was to understand real product data such as prices, discounts, stock availability, and categories by writing practical SQL queries. This project demonstrates data exploration, data cleaning, aggregation, and analytical SQL techniques.

---

## Objective
- Understand product distribution across categories  
- Analyze price and discount patterns  
- Evaluate stock availability and inventory value  
- Practice data cleaning and validation  
- Apply window functions for ranking and comparisons  

---

## Dataset
The data for this project is based on a retail grocery inventory dataset containing product-level information such as name, category, price, discount, stock quantity, and weight.
- Dataset Link: [Zepto Inventory Dataset](https://www.kaggle.com/datasets/palvinder2006/zepto-inventory-dataset)

---

## Schema
```sql
CREATE TABLE zepto_v2 (
    category VARCHAR(120),
    name VARCHAR(150),
    mrp DECIMAL(10,2),
    discountPercent INT,
    availableQuantity INT,
    discountedSellingPrice DECIMAL(10,2),
    weightInGms INT,
    outOfStock BOOLEAN,
    quantity INT
);
```

---

## Business Problems and Solutions

### 1. Count Total Number of Products
```sql
SELECT COUNT(*) AS total_products
FROM zepto_v2;
```
**Objective**
- Determine how many products exist in the dataset

---

### 2. Product Count per Category
```sql
SELECT category, COUNT(*) AS product_count
FROM zepto_v2
GROUP BY category
ORDER BY product_count DESC;
```
**Objective**
- Identify which categories contain the highest number of items

---

### 3. Preview Sample Data
```sql
SELECT *
FROM zepto_v2
LIMIT 8;
```
**Objective**
- Quickly inspect dataset structure and column values

---

### 4. Check Missing Important Values
```sql
SELECT *
FROM zepto_v2
WHERE name IS NULL
   OR mrp IS NULL
   OR category IS NULL;
```
**Objective**
- Detect incomplete or faulty product records

---

### 5. Identify Unique Categories
```sql
SELECT DISTINCT category
FROM zepto_v2
ORDER BY category;
```
**Objective**
- List all available product categories

---

### 6. Stock Availability Distribution
```sql
SELECT outOfStock, COUNT(*) AS item_count
FROM zepto_v2
GROUP BY outOfStock;
```
**Objective**
- Understand how many products are in stock versus out of stock

---

### 7. Most Expensive Products
```sql
SELECT name, mrp
FROM zepto_v2
ORDER BY mrp DESC
LIMIT 10;
```
**Objective**
- Identify premium priced products

---

### 8. Average Selling Price per Category
```sql
SELECT category,
       ROUND(AVG(discountedSellingPrice),2) AS avg_selling_price
FROM zepto_v2
GROUP BY category
ORDER BY avg_selling_price DESC;
```
**Objective**
- Compare pricing trends across categories

---

### 9. Highest Discount Products
```sql
SELECT name, discountPercent
FROM zepto_v2
ORDER BY discountPercent DESC
LIMIT 10;
```
**Objective**
- Discover products offering the biggest discounts

---

### 10. Cheapest Product per Category
```sql
SELECT category,
       MIN(discountedSellingPrice) AS cheapest_item
FROM zepto_v2
GROUP BY category;
```
**Objective**
- Identify the lowest priced item in each category

---

### 11. Price per Gram Value Analysis
```sql
SELECT name,
ROUND(discountedSellingPrice / NULLIF(weightInGms,0),3) AS price_per_gram
FROM zepto_v2
ORDER BY price_per_gram ASC
LIMIT 15;
```
**Objective**
- Find best value for money products

---

### 12. Estimate Total Stock Value per Category
```sql
SELECT category,
       SUM(discountedSellingPrice * availableQuantity) AS stock_value
FROM zepto_v2
GROUP BY category
ORDER BY stock_value DESC;
```
**Objective**
- Calculate potential revenue value of inventory

---

### 13. Rank Products by Price
```sql
SELECT name, mrp,
RANK() OVER (ORDER BY mrp DESC) AS price_rank
FROM zepto_v2;
```
**Objective**
- Assign ranking positions based on product price

---

### 14. Row Number Within Each Category
```sql
SELECT category, name, mrp,
ROW_NUMBER() OVER (PARTITION BY category ORDER BY mrp DESC) AS price_position
FROM zepto_v2;
```
**Objective**
- Understand product positioning inside categories

---

### 15. Running Stock Quantity per Category
```sql
SELECT category, name, availableQuantity,
SUM(availableQuantity) OVER (PARTITION BY category ORDER BY weightInGms) AS running_quantity
FROM zepto_v2;
```
**Objective**
- Track cumulative stock movement in each category

---

## Conclusion
This project helped build a strong foundation in SQL by working with a real-world style inventory dataset. It demonstrates practical skills in querying, aggregating, ranking, and analyzing structured data, which are essential for entry-level data analytics and database roles.
