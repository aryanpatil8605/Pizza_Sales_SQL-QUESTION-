# Pizza Orders Database Queries

## Basic Queries

1. **Retrieve the total number of orders placed:**
    ```sql
    SELECT COUNT(*) AS total_orders FROM orders;
    ```

2. **Calculate the total revenue generated from pizza sales:**
    ```sql
    SELECT SUM(od.quantity * p.price) AS total_revenue
    FROM orders_details od
    JOIN pizzas p ON od.pizza_id = p.pizza_id;
    ```

3. **Identify the highest-priced pizza:**
    ```sql
    SELECT pizza_id, price
    FROM pizzas
    ORDER BY price DESC
    LIMIT 1;
    ```

4. **Identify the most common pizza size ordered:**
    ```sql
    SELECT size, COUNT(*) AS order_count
    FROM pizzas p
    JOIN orders_details od ON p.pizza_id = od.pizza_id
    GROUP BY size
    ORDER BY order_count DESC
    LIMIT 1;
    ```

5. **List the top 5 most ordered pizza types along with their quantities:**
    ```sql
    SELECT pt.name, SUM(od.quantity) AS total_quantity
    FROM orders_details od
    JOIN pizzas p ON od.pizza_id = p.pizza_id
    JOIN pizza_type pt ON p.pizza_type_id = pt.pizza_type_id
    GROUP BY pt.name
    ORDER BY total_quantity DESC
    LIMIT 5;
    ```

## Intermediate Queries

1. **Join the necessary tables to find the total quantity of each pizza category ordered:**
    ```sql
    SELECT pt.category, SUM(od.quantity) AS total_quantity
    FROM orders_details od
    JOIN pizzas p ON od.pizza_id = p.pizza_id
    JOIN pizza_type pt ON p.pizza_type_id = pt.pizza_type_id
    GROUP BY pt.category;
    ```

2. **Determine the distribution of orders by hour of the day:**
    ```sql
    SELECT HOUR(order_time) AS hour, COUNT(*) AS order_count
    FROM orders
    GROUP BY hour
    ORDER BY hour;
    ```

3. **Join relevant tables to find the category-wise distribution of pizzas:**
    ```sql
    SELECT pt.category, COUNT(*) AS order_count
    FROM orders_details od
    JOIN pizzas p ON od.pizza_id = p.pizza_id
    JOIN pizza_type pt ON p.pizza_type_id = pt.pizza_type_id
    GROUP BY pt.category;
    ```

4. **Group the orders by date and calculate the average number of pizzas ordered per day:**
    ```sql
    SELECT order_date, AVG(total_pizzas) AS avg_pizzas_per_day
    FROM (
        SELECT order_date, SUM(od.quantity) AS total_pizzas
        FROM orders o
        JOIN orders_details od ON o.order_id = od.order_id
        GROUP BY order_date
    ) AS daily_orders
    GROUP BY order_date;
    ```

5. **Determine the top 3 most ordered pizza types based on revenue:**
    ```sql
    SELECT pt.name, SUM(od.quantity * p.price) AS total_revenue
    FROM orders_details od
    JOIN pizzas p ON od.pizza_id = p.pizza_id
    JOIN pizza_type pt ON p.pizza_type_id = pt.pizza_type_id
    GROUP BY pt.name
    ORDER BY total_revenue DESC
    LIMIT 3;
    ```

## Advanced Queries

1. **Calculate the percentage contribution of each pizza type to total revenue:**
    ```sql
    SELECT pt.name, 
           SUM(od.quantity * p.price) / (SELECT SUM(od.quantity * p.price) FROM orders_details od JOIN pizzas p ON od.pizza_id = p.pizza_id) * 100 AS percentage_contribution
    FROM orders_details od
    JOIN pizzas p ON od.pizza_id = p.pizza_id
    JOIN pizza_type pt ON p.pizza_type_id = pt.pizza_type_id
    GROUP BY pt.name;
    ```

2. **Analyze the cumulative revenue generated over time:**
    ```sql
    SELECT order_date, SUM(od.quantity * p.price) OVER (ORDER BY order_date) AS cumulative_revenue
    FROM orders o
    JOIN orders_details od ON o.order_id = od.order_id
    JOIN pizzas p ON od.pizza_id = p.pizza_id;
    ```

3. **Determine the top 3 most ordered pizza types based on revenue for each pizza category:**
    ```sql
    SELECT pt.category, pt.name, SUM(od.quantity * p.price) AS total_revenue
    FROM orders_details od
    JOIN pizzas p ON od.pizza_id = p.pizza_id
    JOIN pizza_type pt ON p.pizza_type_id = pt.pizza_type_id
    GROUP BY pt.category, pt.name
    ORDER BY pt.category, total_revenue DESC
    LIMIT 3;
    ```
