# Sql-Project-Pizza-Sales
Pizza Sales Analysis
Skills Used: SQL, Python, Power BI
Technologies: MySQL, Power BI

Description:
## Basic Queries

1. **Retrieve the total number of orders placed**:
```sql
SELECT COUNT(*) AS total_orders
FROM orders;
```

2. **Calculate the total revenue generated from pizza sales**:
```sql
SELECT SUM(quantity * price) AS total_revenue
FROM order_details
JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id;
```

3. **Identify the highest-priced pizza**:
```sql
SELECT pizza_name, MAX(price) AS highest_price
FROM pizzas;
```

4. **Identify the most common pizza size ordered**:
```sql
SELECT size, COUNT(*) AS order_count
FROM pizzas
GROUP BY size
ORDER BY order_count DESC
LIMIT 1;
```

5. **List the top 5 most ordered pizza types along with their quantities**:
```sql
SELECT pizza_name, SUM(quantity) AS total_quantity
FROM order_details
JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id
GROUP BY pizza_name
ORDER BY total_quantity DESC
LIMIT 5;
```


## Intermediate Queries

1. **Find the total quantity of each pizza category ordered**:
```sql
SELECT pizza_category, SUM(quantity) AS total_quantity
FROM order_details
JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id
GROUP BY pizza_category;
```

2. **Determine the distribution of orders by hour of the day**:
```sql
SELECT HOUR(order_time) AS order_hour, COUNT(*) AS order_count
FROM orders
GROUP BY order_hour;
```

3. **Category-wise distribution of pizzas**:
```sql
SELECT pizza_category, COUNT(*) AS total_orders
FROM order_details
JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id
GROUP BY pizza_category;
```

4. **Group orders by date and calculate the average number of pizzas ordered per day**:
```sql
SELECT order_date, AVG(quantity) AS avg_pizzas_per_day
FROM orders
JOIN order_details ON orders.order_id = order_details.order_id
GROUP BY order_date;
```

5. **Determine the top 3 most ordered pizza types based on revenue**:
```sql
SELECT pizza_name, SUM(quantity * price) AS revenue
FROM order_details
JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id
GROUP BY pizza_name
ORDER BY revenue DESC
LIMIT 3;
```


## Advanced Queries

1. **Calculate the percentage contribution of each pizza type to total revenue**:
```sql
SELECT pizza_name, (SUM(quantity * price) / (SELECT SUM(quantity * price) FROM order_details JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id) * 100) AS percentage_contribution
FROM order_details
JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id
GROUP BY pizza_name;
```

2. **Analyze cumulative revenue generated over time**:
```sql
SELECT order_date, SUM(quantity * price) OVER (ORDER BY order_date) AS cumulative_revenue
FROM orders
JOIN order_details ON orders.order_id = order_details.order_id
JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id;
```

3. **Determine the top 3 most ordered pizza types based on revenue for each pizza category**:
```sql
SELECT pizza_category, pizza_name, SUM(quantity * price) AS revenue
FROM order_details
JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id
GROUP BY pizza_category, pizza_name
ORDER BY pizza_category, revenue DESC
LIMIT 3;
```

