# Zepto Inventory SQL Analysis

## Overview
This project is about exploring and analyzing a grocery inventory dataset using SQL. The main aim was to understand how real product data works such as prices, discounts, stock availability, and categories by writing practical SQL queries. Through this project I practiced cleaning data, grouping information, and finding useful insights from raw inventory data.

## Objective
Understand how products are distributed across categories  
Observe price and discount patterns  
Analyze stock availability  
Clean missing or incorrect data  
Use window functions to rank and compare products  

## Dataset
The dataset contains product level inventory information such as Product Name, Category, Price, Discount Percentage, Discounted Selling Price, Available Quantity, Product Weight in grams, and Stock Status.

## Business Questions and Queries

-- checking total number of products  
SELECT COUNT(*) AS total_products FROM zepto_v2;

-- identifying product count per category  
SELECT category, COUNT(*) AS product_count FROM zepto_v2 GROUP BY category ORDER BY product_count DESC;

-- previewing initial rows of data  
SELECT * FROM zepto_v2 LIMIT 8;

-- checking for missing important values  
SELECT * FROM zepto_v2 WHERE name IS NULL OR mrp IS NULL OR category IS NULL;

-- identifying all unique categories  
SELECT DISTINCT category FROM zepto_v2 ORDER BY category;

-- checking stock availability distribution  
SELECT outOfStock, COUNT(*) AS item_count FROM zepto_v2 GROUP BY outOfStock;

-- identifying the most expensive products  
SELECT name, mrp FROM zepto_v2 ORDER BY mrp DESC LIMIT 10;

-- calculating average selling price per category  
SELECT category, ROUND(AVG(discountedSellingPrice),2) AS avg_selling_price FROM zepto_v2 GROUP BY category ORDER BY avg_selling_price DESC;

-- identifying products with very high discounts  
SELECT name, discountPercent FROM zepto_v2 WHERE discountPercent > 50 ORDER BY discountPercent DESC;

-- checking products with highest stock quantity  
SELECT name, availableQuantity FROM zepto_v2 ORDER BY availableQuantity DESC LIMIT 10;

-- identifying cheapest products in each category  
SELECT category, MIN(discountedSellingPrice) AS cheapest_item FROM zepto_v2 GROUP BY category;

-- calculating value for money using price per gram  
SELECT name, ROUND(discountedSellingPrice / NULLIF(weightInGms,0), 3) AS price_per_gram FROM zepto_v2 ORDER BY price_per_gram ASC LIMIT 15;

-- categorizing products based on weight range  
SELECT name, CASE WHEN weightInGms < 500 THEN 'Small Pack' WHEN weightInGms < 2000 THEN 'Medium Pack' ELSE 'Large Pack' END AS pack_type FROM zepto_v2;

-- estimating total stock value per category  
SELECT category, SUM(discountedSellingPrice * availableQuantity) AS stock_value FROM zepto_v2 GROUP BY category ORDER BY stock_value DESC;

-- Row number of products within each category based on price  
SELECT category, name, mrp, ROW_NUMBER() OVER (PARTITION BY category ORDER BY mrp DESC) AS price_position FROM zepto_v2;

-- Rank products by MRP highest price first  
SELECT name, mrp, RANK() OVER (ORDER BY mrp DESC) AS price_rank FROM zepto_v2;

-- Dense rank products by discount percentage  
SELECT name, discountPercent, DENSE_RANK() OVER (ORDER BY discountPercent DESC) AS discount_rank FROM zepto_v2;

-- Running total of available quantity within each category  
SELECT category, name, weightInGms, availableQuantity, SUM(availableQuantity) OVER (PARTITION BY category ORDER BY weightInGms) AS running_quantity FROM zepto_v2;

-- Total stock quantity within each category  
SELECT category, name, availableQuantity, SUM(availableQuantity) OVER (PARTITION BY category) AS total_category_quantity FROM zepto_v2;

## Conclusion
Working on this project helped me understand how SQL is used in real situations. I learned how to explore datasets, clean incorrect values, group information, and use window functions to gain deeper insights. This project gave me practical hands on experience and built a strong base in SQL for future data analytics and database roles.
