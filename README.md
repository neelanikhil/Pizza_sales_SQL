# 🍕 Pizza Sales Analysis - SQL Project

![Pizza Logo](https://raw.githubusercontent.com/YourGitHubUsername/YourRepositoryName/main/pizza_logo.png)


## 📌 Project Overview
This project is part of my portfolio, showcasing SQL skills in **data analysis** and **business intelligence**. Using SQL queries, I explored **pizza sales data** to gain insights into order trends, revenue generation, peak sales hours, and customer preferences. 

The insights obtained can help businesses **optimize inventory**, **improve marketing strategies**, and **increase overall profitability**.

---

## 🎯 Objectives
The key objectives of this project are:
✅ **Calculate total revenue** generated from pizza sales.  
✅ **Identify the highest-priced pizza** in the menu.  
✅ **Determine the most common pizza size ordered** by customers.  
✅ **Analyze order distribution by hour of the day** to find peak sales times.  
✅ **Find category-wise distribution of pizzas** using SQL JOINs.  
✅ **Analyze cumulative revenue growth over time**.  
✅ **Identify the top 3 best-selling pizza types** based on revenue.  

---

## 🗂 Dataset Information
The dataset consists of the following key tables:

- `orders` - Contains order details with timestamps.
- `order_details` - Links orders to pizzas with quantity information.
- `pizzas` - Contains pizza pricing and size details.
- `pizza_types` - Lists the category and name of different pizza types.

---

## 📊 SQL Queries Used
Here are some key SQL queries used in the analysis:

### **1️ Total Number of Orders**
```sql
SELECT COUNT(order_id) AS total_orders FROM orders;
```
**objective** To determine the total number of orders received, helping businesses track overall order volume and assess customer demand trends.

## 2.Calculate the Total Revenue Generated from Pizza Sales
```sql
SELECT 
    ROUND(SUM(order_details.quantity * pizzas.price), 2) AS total_sales
FROM order_details
JOIN pizzas ON pizzas.pizza_id = order_details.pizza_id;
```
**objective** To calculate the total revenue generated from pizza sales by multiplying the quantity of pizzas sold with their respective prices. This insight helps in evaluating business performance and profitability.

## 3.Identify the Highest-Priced Pizza
```sql
SELECT 
    pizza_types.name, pizzas.price
FROM pizza_types
JOIN pizzas ON pizza_types.pizza_type_id = pizzas.pizza_type_id
ORDER BY pizzas.price DESC
LIMIT 1;
```
**objective** To find the most expensive pizza available on the menu, which can help in pricing strategy decisions and analyzing high-end product offerings.

## 4. Identify the Most Common Pizza Size Ordered
```sql
SELECT 
    pizzas.size, COUNT(order_details.order_details_id) AS order_count
FROM pizzas
JOIN order_details ON pizzas.pizza_id = order_details.pizza_id
GROUP BY pizzas.size
ORDER BY order_count DESC
LIMIT 1;
```
**objective** To determine the most frequently ordered pizza size, allowing businesses to optimize inventory, adjust pricing, and streamline production based on customer preferences.

## 5.Total Quantity of Each Pizza Category Ordered
```sql
SELECT 
    pizza_types.category,
    SUM(order_details.quantity) AS quantity
FROM pizza_types
JOIN pizzas ON pizza_types.pizza_type_id = pizzas.pizza_type_id
JOIN order_details ON order_details.pizza_id = pizzas.pizza_id
GROUP BY pizza_types.category
ORDER BY quantity DESC;
```
**objective** To analyze the distribution of pizza orders by category (e.g., Veg, Non-Veg, Specialty) and identify which category generates the highest sales.

## 6.Determine the Distribution of Orders by Hour of the Day
```sql
SELECT 
    HOUR(order_time) AS hour, COUNT(order_id) AS order_count
FROM orders
GROUP BY HOUR(order_time);
```
**objective** To understand customer ordering patterns by identifying peak and off-peak hours, which can help in staffing, marketing, and operational efficiency.

## 7.Join Relevant Tables to Find the Category-Wise Distribution of Pizzas
```sql
SELECT category, COUNT(name) FROM pizza_types
GROUP BY category;
```
**objective** To determined the total number of pizza varieties available in each category, which helps in menu optimization and inventory planning.

## 8.Group the Orders by Date and Calculate the Average Number of Pizzas Ordered Per Day
```sql
SELECT 
    ROUND(AVG(quantity), 0) AS avg_pizza_order_per_day
FROM
    (SELECT 
        orders.order_date, SUM(order_details.quantity) AS quantity
    FROM orders
    JOIN order_details ON orders.order_id = order_details.order_id
    GROUP BY orders.order_date) AS order_quantity;
```
**objective** To analyze the average daily demand for pizzas, allowing businesses to predict sales trends and optimize inventory.

## 9.Analyze the Cumulative Revenue Generated Over Time
```sql
SELECT order_date, SUM(revenue) OVER(ORDER BY order_date) AS cum_revenue 
FROM (
    SELECT orders.order_date,
    SUM(order_details.quantity * pizzas.price) AS revenue
    FROM order_details 
    JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id 
    JOIN orders ON orders.order_id = order_details.order_id
    GROUP BY orders.order_date
) AS sales;
```
**objective** To track cumulative revenue growth over time, helping businesses analyze long-term financial trends and make informed strategic decisions.




