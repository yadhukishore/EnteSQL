No, DBMS (Database Management System) and RDBMS (Relational Database Management System) are not the same, although they are related concepts.

**DBMS (Database Management System):**
- DBMS is a software system that allows users to create, manage, and manipulate databases.
- It provides tools and utilities for storing, retrieving, updating, and deleting data in a database.
- DBMS can support various data models, including hierarchical, network, and relational models.
- Examples of DBMS include MongoDB (NoSQL), Apache Cassandra, and Redis.

**RDBMS (Relational Database Management System):**
- RDBMS is a specific type of DBMS that is based on the relational model of data organization.
- It organizes data into tables consisting of rows and columns, with relationships defined between tables.
- RDBMS enforces integrity constraints such as primary keys, foreign keys, and referential integrity to maintain data consistency and integrity.
- SQL (Structured Query Language) is the standard language used to interact with RDBMS.
- Examples of RDBMS include MySQL, PostgreSQL, Oracle Database, SQL Server, and SQLite.

In summary, while RDBMS is a type of DBMS specifically designed for managing relational databases, not all DBMS are relational. RDBMS adheres to the relational model and implements features such as tables, rows, columns, and relationships, whereas DBMS can support various data models beyond the relational model.

## Which will choose
The choice between using a DBMS (Database Management System) and an RDBMS (Relational Database Management System) depends on several factors, including the nature of your data, the complexity of your data relationships, scalability requirements, and the need for data integrity and consistency. Here's when you might consider using each:

**Use DBMS (Database Management System) when:**
1. You have data that doesn't fit well into the tabular structure of traditional relational databases.
2. Your application requires handling semi-structured or unstructured data, such as JSON or XML documents.
3. You need a highly scalable and flexible database solution that can easily accommodate changes in data structure.
4. You're building real-time analytics, content management systems, or applications with rapidly changing data requirements.
5. You want to take advantage of features like sharding, replication, and horizontal scaling to distribute data across multiple nodes.

**Use RDBMS (Relational Database Management System) when:**
1. Your data has a well-defined structure with clear relationships between entities, such as customers, orders, and products.
2. You require strict data integrity and consistency, enforced through features like primary keys, foreign keys, and transactions.
3. You need support for complex queries and joins, typical in business intelligence, reporting, and data analysis applications.
4. Your application demands ACID (Atomicity, Consistency, Isolation, Durability) compliance for transactions.
5. You're developing traditional business applications, e-commerce platforms, financial systems, or applications with standardized data models.

In summary, choose a DBMS like MongoDB or Apache Cassandra when dealing with flexible, rapidly changing data and scalability is a top priority. Choose an RDBMS like MySQL or PostgreSQL when data structure, integrity, and relational queries are essential for your application's functionality and performance.


# Constraints


**Constraints** are like rules that you set for your data in a table. These rules make sure that the data in your table is accurate and reliable.

Imagine you have a table with different columns like name, age, and email. Now, you want to make sure that only certain types of data can go into each column. For example, the age column should only have numbers, and the email column should only have valid email addresses. That's where constraints come in.

**Column Level Constraints**: These are rules that you apply to each individual column. For example, you can say that the age column must always have numbers, or the email column must always have valid email addresses.

**Table Level Constraints**: These are rules that apply to the entire table. For example, you can say that no two rows in the table should have the same value in the name column.

By applying these constraints, you ensure that the data in your database is accurate, reliable, and consistent, which makes it easier to work with and trust. Constraints help maintain the quality of your data and prevent errors or inconsistencies.
## Practical


Suppose we have a table named `employees` with the following structure:

```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50) NOT NULL,
    emp_age INT,
    emp_email VARCHAR(100) UNIQUE
);
```

In this table:
- `emp_id` is the primary key, ensuring each employee has a unique identifier.
- `emp_name` is a required field (`NOT NULL` constraint), meaning it cannot be empty.
- `emp_age` is optional, allowing for NULL values.
- `emp_email` must be unique for each employee (`UNIQUE` constraint), preventing duplicate email addresses.

Let's insert some data into this table:

```sql
INSERT INTO employees (emp_id, emp_name, emp_age, emp_email)
VALUES
(1, 'John', 30, 'john@example.com'),
(2, 'Jane', NULL, 'jane@example.com'),
(3, 'Mike', 45, 'mike@example.com');
```

Now, let's try to insert a new employee with the same email address as an existing employee:

```sql
INSERT INTO employees (emp_id, emp_name, emp_age, emp_email)
VALUES
(4, 'Sarah', 28, 'john@example.com'); -- This will fail due to UNIQUE constraint violation
```

This insert operation will fail because the email address 'john@example.com' already exists in the `emp_email` column, violating the UNIQUE constraint.

Next, let's demonstrate a table-level constraint. Suppose we want to ensure that the age of each employee is between 18 and 65. We can define a check constraint at the table level to enforce this rule:

```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50) NOT NULL,
    emp_age INT CHECK (emp_age >= 18 AND emp_age <= 65), -- Table-level constraint
    emp_email VARCHAR(100) UNIQUE
);
```

With this check constraint, any attempt to insert or update an employee's age outside the specified range will be rejected by the database.

By applying these constraints, we ensure the accuracy, reliability, and consistency of the data in our `employees` table.

# Normalisation

**Database normalization is the process of efficiently organizing data in a database to eliminate the redundant data from the database and ensuring data dependencies make sense. Various Normalization Forms are used to eliminate or reduce data redundancy in database tables.**

1nf

*Theory:-*  https://www.tutorialspoint.com/sql/first-normal-form.htm

## practical (1nf)

Sure, let's transform the given table into the first normal form (1NF) using practical SQL queries.

Consider the original `CUSTOMERS` table:

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(50),
    city VARCHAR(50)
);
```

This table violates the first normal form because the `city` column can contain multiple values.

To bring this table to 1NF, we'll split it into two separate tables: `customers` and `customer_cities`.

First, let's create the `customers` table, which will store unique customer information:

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(50)
);
```

Next, we'll create the `customer_cities` table to store the cities associated with each customer:

```sql
CREATE TABLE customer_cities (
    customer_id INT,
    city VARCHAR(50),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```

Now, let's insert data into these tables. First, we'll insert customer information into the `customers` table:

```sql
INSERT INTO customers (customer_id, customer_name)
VALUES
(1, 'John'),
(2, 'Jane'),
(3, 'Mike');
```

Next, we'll insert city information into the `customer_cities` table:

```sql
INSERT INTO customer_cities (customer_id, city)
VALUES
(1, 'Hyderabad'),
(1, 'Delhi'),
(2, 'New York'),
(3, 'London');
```

Now, we have successfully transformed the original table into 1NF. The `customers` table contains unique customer information, and the `customer_cities` table stores the cities associated with each customer, avoiding repeating groups of data.

This ensures that every column of a table contains only atomic values, fulfilling the requirements of the first normal form (1NF).

##  2NF:-

Let's simplify the concept of the Second Normal Form (2NF):

**Second Normal Form (2NF):**

1. **Meet 1NF Requirements:** Before achieving 2NF, the table must already meet all the rules of the First Normal Form (1NF), which include having atomic values in each column and no repeating groups of data.

2. **No Partial Dependencies:** In 2NF, there should be no partial dependencies of any non-key columns on part of the primary key. This means that every non-key column should be fully dependent on the entire primary key, not just part of it.

**Example:**

Consider a table that stores customer and order information:

```sql
CREATE TABLE customer_orders (
   customer_id INT NOT NULL,
   customer_name VARCHAR(20) NOT NULL,
   order_id INT NOT NULL,
   order_detail VARCHAR(20) NOT NULL,
   sale_date DATETIME,
   PRIMARY KEY (customer_id, order_id)
);
```

In this table:
- `customer_id` and `order_id` together form the primary key, ensuring unique combinations of customers and orders.
- However, `customer_name`, `order_detail`, and `sale_date` are not fully dependent on both `customer_id` and `order_id`.
- `customer_name` depends only on `customer_id`, and `order_detail` and `sale_date` depend only on `order_id`.

To achieve 2NF, we need to split this table into multiple tables to eliminate partial dependencies:

1. **Customers Table:**
```sql
CREATE TABLE customers (
   customer_id INT PRIMARY KEY,
   customer_name VARCHAR(20) NOT NULL
);
```

2. **Orders Table:**
```sql
CREATE TABLE orders (
   order_id INT PRIMARY KEY,
   order_detail VARCHAR(20) NOT NULL,
   sale_date DATETIME
);
```

3. **CustomerOrders Table:**
```sql
CREATE TABLE customer_orders (
   customer_id INT NOT NULL,
   order_id INT NOT NULL,
   PRIMARY KEY (customer_id, order_id),
   FOREIGN KEY (customer_id) REFERENCES customers(customer_id),
   FOREIGN KEY (order_id) REFERENCES orders(order_id)
);
```

Now, each table has a clear purpose, and there are no partial dependencies between columns and parts of the primary key, satisfying the requirements of 2NF.

*Check 3nf in the link*
# joins
Let's simplify the concept of SQL joins:

**SQL Joins:**

SQL joins are used to combine data from two or more tables based on a related column between them. Joins help in retrieving records by linking fields from different tables using their foreign keys.

**Basic Syntax:**
```
SELECT column_name(s)
FROM table1
JOIN table2
ON table1.column_name = table2.column_name;
```

**Example:**

Consider two tables: `customers` and `orders`.

```sql
CREATE TABLE customers (
   id INT PRIMARY KEY,
   name VARCHAR(20) NOT NULL,
   age INT NOT NULL
);

CREATE TABLE orders (
   order_id INT PRIMARY KEY,
   order_date DATE NOT NULL,
   customer_id INT NOT NULL,
   amount DECIMAL(18, 2)
);
```

**Inner Join:**

An inner join retrieves records that have matching values in both tables.

```sql
SELECT c.id, c.name, c.age, o.amount 
FROM customers c
JOIN orders o
ON c.id = o.customer_id;
```

**Outer Join:**

- **Left Join:** Returns all rows from the left table and the matched rows from the right table. If there is no match, NULL values are returned for the right table columns.

```sql
SELECT c.id, c.name, c.age, o.amount 
FROM customers c
LEFT JOIN orders o
ON c.id = o.customer_id;
```

- **Right Join:** Returns all rows from the right table and the matched rows from the left table. If there is no match, NULL values are returned for the left table columns.

```sql
SELECT c.id, c.name, c.age, o.amount 
FROM customers c
RIGHT JOIN orders o
ON c.id = o.customer_id;
```

- **Full Join:** Returns all rows when there is a match in one of the tables. If there is no match, NULL values are returned for unmatched columns.

**Other Joins:**

- **Self Join:** Used to join a table to itself as if the table were two tables, allowing comparisons within the same table.

- **Cross Join:** Returns the Cartesian product of the sets of records from the two or more joined tables, resulting in all possible combinations of rows.

By understanding and utilizing these SQL joins, you can effectively retrieve and combine data from multiple tables based on the specified conditions.
