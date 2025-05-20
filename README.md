# Pizza-sales-Dashboard
I built this Power BI dashboard to analyze trends in pizza sales. The data, sourced from the pizza_sales table, was processed using SQL queries and then visualized to highlight key business insights.
![image](https://github.com/user-attachments/assets/eb1cd0ff-d754-455b-871c-18f542c6131f)
### A. KPI’s

1. **Total Revenue:**
   - SQL Query: `SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;`

2. **Average Order Value:**
   - SQL Query: `SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales`

3. **Total Pizzas Sold:**
   - SQL Query: `SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales`

4. **Total Orders:**
   - SQL Query: `SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales`

5. **Average Pizzas Per Order:**
   - SQL Query: 
     ```sql
     SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
     CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
     AS Avg_Pizzas_per_order
     FROM pizza_sales
     ```

### B. Daily Trend for Total Orders

   - SQL Query: 
     ```sql
     SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
     FROM pizza_sales
     GROUP BY DATENAME(DW, order_date)
     ```



### C. Monthly Trend for Orders

   - SQL Query: 
     ```sql
     SELECT DATENAME(MONTH, order_date) as Month_Name, COUNT(DISTINCT order_id) as Total_Orders
     FROM pizza_sales
     GROUP BY DATENAME(MONTH, order_date)
     ```

 
### D. % of Sales by Pizza Category

   - SQL Query: 
     ```sql
     SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
     CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
     FROM pizza_sales
     GROUP BY pizza_category
     ```


### E. % of Sales by Pizza Size

   - SQL Query: 
     ```sql
     SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
     CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
     FROM pizza_sales
     GROUP BY pizza_size
     ORDER BY pizza_size
     ```


## Top and Bottom Performers

### F. Total Pizzas Sold by Pizza Category

   - SQL Query: 
     ```sql
     SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
     FROM pizza_sales
     WHERE MONTH(order_date) = 2
     GROUP BY pizza_category
     ORDER BY Total_Quantity_Sold DESC
     ```


### G. Top 5 Pizzas by Revenue

   - SQL Query: 
     ```sql
     SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
     FROM pizza_sales
     GROUP BY pizza_name
     ORDER BY Total_Revenue DESC
     ```

### H. Bottom 5 Pizzas by Revenue

   - SQL Query: 
     ```sql
     SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
     FROM pizza_sales
     GROUP BY pizza_name
     ORDER BY Total_Revenue ASC
     ```


### I. Top 5 Pizzas by Quantity

   - SQL Query: 
     ```sql
     SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
     FROM pizza_sales
     GROUP BY pizza_name
     ORDER BY Total_Pizza_Sold DESC
     ```


### J. Bottom 5 Pizzas by Quantity

   - SQL Query: 
     ```sql
     SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
     FROM pizza_sales
     GROUP BY pizza_name
     ORDER BY Total_Pizza_Sold ASC
     ```


### K. Top 5 Pizzas by Total Orders

   - SQL Query: 
     ```sql
     SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
     FROM pizza_sales
     GROUP BY pizza_name
     ORDER BY Total_Orders DESC
     ```

### L. Bottom 5 Pizzas by Total Orders

   - SQL Query: 
     ```sql
     SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
     FROM pizza_sales
     GROUP BY pizza_name
     ORDER BY Total_Orders ASC
     ```


## Applying Filters

If you want to apply filters to the above queries, you can use the `WHERE` clause in SQL. For example:

```sql
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
WHERE pizza_category = 'Classic'
GROUP BY pizza_name
ORDER BY Total_Orders ASC
```

Feel free to explore and customize the report based on your specific requirements!

