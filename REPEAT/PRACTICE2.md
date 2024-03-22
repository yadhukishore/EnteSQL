

# SQL Practice Questions

Here are some practical SQL questions for you to work on:

## 1. Retrieve all columns from the `employees` table:

```sql
SELECT * FROM employees;
```

## 2. Retrieve the names and salaries of all employees earning more than $50,000:

```sql
SELECT name, salary
FROM employees
WHERE salary > 50000;
```

## 3. List the departments along with the number of employees in each department:

```sql
SELECT department_id, COUNT(id) AS num_employees
FROM employees
GROUP BY department_id;
```

## 4. Find the total number of orders placed in the `orders` table:

```sql
SELECT COUNT(order_id) AS total_orders FROM orders;
```

## 5. Retrieve the names of customers who have placed orders:

```sql
SELECT c.name AS customer_name
FROM customer c
JOIN orders o ON c.customer_id = o.customer_id;
```

## 6. Calculate the total revenue generated from orders in the past month:

```sql
SELECT SUM(price) AS totalRevenue
FROM  orders
WHERE orders_date >= DATE_SUB(NOW(), INTERVAL 1 MONTH);
```

## 7. List the products along with their prices and quantities in stock:

```sql
SELECT product_name AS p_name, price AS Amount, quantity_in_stock AS Quantity
FROM products;
```

## 8. Find the average salary of employees in each department:

```sql
SELECT d.department_name, AVG(e.salary) AS avg_salary
FROM employees e
JOIN department d ON e.department_id = d.department_id
GROUP BY d.department_name;
```

## 9. Retrieve the names of employees whose hire date is in the year 2019:

```sql
SELECT names 
FROM employees
WHERE YEAR(hire_date) = 2019;
```

## 10. List the orders placed by customers from a specific country:

```sql
SELECT c.customer_id, c.customer_name, o.order_id
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
WHERE country = "Germany";
```


