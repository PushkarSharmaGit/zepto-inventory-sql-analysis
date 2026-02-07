# Zepto Inventory SQL Analysis

## Overview
This project focuses on exploring and analyzing a grocery inventory dataset using SQL.  
The goal was to understand real product data such as prices, discounts, stock availability, and categories by writing practical SQL queries.  
Through this project I practiced cleaning data, grouping information, and extracting useful insights from raw inventory data.

---

## Objective
- Understand product distribution across categories
- Observe price and discount trends
- Analyze stock availability
- Practice SQL data cleaning
- Use window functions for ranking and comparisons

---

## Dataset
The dataset contains product level inventory data including:
- Product Name
- Category
- Price (MRP)
- Discount Percentage
- Discounted Selling Price
- Available Quantity
- Product Weight (grams)
- Stock Status

---

## Schema

### Columns

- `category` – Product category  
- `name` – Product name  
- `mrp` – Maximum retail price  
- `discountPercent` – Discount percentage  
- `availableQuantity` – Quantity in stock  
- `discountedSellingPrice` – Final selling price  
- `weightInGms` – Product weight in grams  
- `outOfStock` – Stock availability status  
- `quantity` – SKU quantity  

---

### SQL Table Creation Code

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
