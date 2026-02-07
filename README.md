Overview
This project is about exploring and analyzing a grocery inventory dataset using SQL. 
The main goal was to understand how product data works in a real-world scenario — things like prices, discounts, stock availability, and categories. 
Through this project, I practiced writing SQL queries to clean data, group information, and find useful insights from raw inventory data.

Objective
- Understand how products are spread across different categories
- Observe price and discount patterns
- Check stock availability
- Clean missing or incorrect data
- Use window functions to rank and compare products

Dataset
The dataset contains product-level inventory information such as:
- Product Name
- Category
- MRP (Price)
- Discount Percentage
- Discounted Selling Price
- Available Quantity
- Product Weight (grams)
- Stock Status

Schema
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

Business Questions & Queries

1. Count Total Products  
SELECT COUNT(*) FROM zepto_v2;  
Purpose: Find out how many products are in the dataset.

2. Products per Category  
SELECT category, COUNT(*) FROM zepto_v2 GROUP BY category;  
Purpose: See which categories have the most items.

3. Preview Sample Data  
SELECT * FROM zepto_v2 LIMIT 8;  
Purpose: Quickly check what the dataset looks like.

4. Check Missing Values  
SELECT * FROM zepto_v2  
WHERE name IS NULL OR mrp IS NULL OR category IS NULL;  
Purpose: Identify incomplete or missing data.

5. Unique Categories  
SELECT DISTINCT category FROM zepto_v2;  
Purpose: List all available product categories.

6. Stock Availability Count  
SELECT outOfStock, COUNT(*) FROM zepto_v2 GROUP BY outOfStock;  
Purpose: Compare how many products are in stock vs out of stock.

7. Most Expensive Products  
SELECT name, mrp FROM zepto_v2 ORDER BY mrp DESC LIMIT 10;  
Purpose: Identify high-priced products.

8. Average Price per Category  
SELECT category, AVG(discountedSellingPrice)  
FROM zepto_v2 GROUP BY category;  
Purpose: Understand pricing trends in each category.

9. Highest Discounts  
SELECT name, discountPercent  
FROM zepto_v2 ORDER BY discountPercent DESC;  
Purpose: Find products with the biggest discounts.

10. Cheapest Product per Category  
SELECT category, MIN(discountedSellingPrice)  
FROM zepto_v2 GROUP BY category;  
Purpose: Identify low-cost options in each category.

11. Price per Gram (Value for Money)  
SELECT name, discountedSellingPrice / NULLIF(weightInGms,0)  
FROM zepto_v2;  
Purpose: Compare actual value based on weight.

12. Stock Value per Category  
SELECT category,  
SUM(discountedSellingPrice * availableQuantity)  
FROM zepto_v2 GROUP BY category;  
Purpose: Estimate how much inventory value each category holds.

13. Rank Products by Price  
SELECT name, mrp,  
RANK() OVER (ORDER BY mrp DESC)  
FROM zepto_v2;  
Purpose: Rank products from highest to lowest price.

14. Number Products Inside Categories  
SELECT category, name,  
ROW_NUMBER() OVER (PARTITION BY category ORDER BY mrp DESC)  
FROM zepto_v2;  
Purpose: Give each product a position inside its category.

15. Running Stock Quantity  
SELECT category, name,  
SUM(availableQuantity) OVER (PARTITION BY category)  
FROM zepto_v2;  
Purpose: View total stock accumulation within each category.

Conclusion
Working on this project helped me understand how SQL is used in real situations. 
I learned how to explore datasets, clean incorrect values, group information, and apply window functions to get deeper insights. 
This project gave me practical hands-on experience and built a strong foundation in SQL for future data analytics and database work.
