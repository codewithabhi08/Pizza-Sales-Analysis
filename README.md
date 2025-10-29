# Pizza-Sales-Analysis

### 📖 Overview
This project focuses on analyzing pizza store sales data using SQL and Excel to generate meaningful business insights.  
It’s an end-to-end analysis project covering data cleaning, KPI calculations, trend analysis, and dashboard creation.

---

### 🎯 Project Goals
- Calculate key performance metrics like Total Revenue, Total Orders, and Average Order Value  
- Identify order trends by day of week and hour of day  
- Analyze sales contribution by pizza category and size  
- Find top and bottom-performing pizzas  
- Build a dynamic Excel dashboard to present the findings

---

### 🧰 Tools & Technologies
- **SQL Server** – for data exploration and querying  
- **Microsoft Excel** – for visualization and dashboard building  
- **CSV Dataset** – pizza sales data (orders, pizzas, quantities, revenue)

---

### 📊 Dataset Description
The dataset (`pizza_sales.csv`) contains:
- `order_id`, `order_date`, `order_time`  
- `pizza_name`, `pizza_category`, `pizza_size`  
- `quantity`, `unit_price`, `total_price`  

---

### 🔍 Key SQL Queries
```sql
-- Total Revenue
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;

-- Average Order Value
SELECT (SUM(total_price)/COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales;

-- Daily Order Trend
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders
FROM pizza_sales
GROUP BY DATENAME(DW, order_date);

-- Sales by Category
SELECT pizza_category, SUM(total_price) AS total_revenue
FROM pizza_sales
GROUP BY pizza_category;

-- Average Pizzas Per Order
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS Avg_Pizzas_per_order
FROM pizza_sales

-- Percentage of Sales by Pizza Category :
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category

-- Top 5 Best Sellers by Total Pizzas Sold :
SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC

-- Bottom 5 Best Sellers by Total Pizzas Sold :
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC

