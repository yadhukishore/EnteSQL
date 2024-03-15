# 2.Order Management



2. **Order Management:**
   - Consider a database for managing orders. You have two tables: `orders` and `customers`. The `orders` table has a foreign key `customer_id` referencing the `customer_id` in the `customers` table.
   - Question: How would you design the schema to ensure that an order can only be associated with an existing customer using foreign keys?

3. **Product Inventory:**
   - Suppose you have tables for managing product inventory: `products` and `suppliers`. The `products` table has a foreign key `supplier_id` referencing the `supplier_id` in the `suppliers` table.
   - Question: How can you ensure that each product is associated with a valid supplier using foreign keys?

4. **Student Enrollment:**
   - Imagine a university database with tables for students (`students`) and courses (`courses`). The `students` table has a foreign key `course_id` referencing the `course_id` in the `courses` table.
   - Question: How would you structure the database to ensure that each student is enrolled in an existing course using foreign keys?

5. **Library Management:**
   - Consider a library database with tables for books (`books`) and authors (`authors`). The `books` table has a foreign key `author_id` referencing the `author_id` in the `authors` table.
   - Question: How can you guarantee that each book in the library is authored by an existing author using foreign keys?

These questions illustrate the practical application of foreign keys and primary keys in ensuring data integrity and maintaining relationships between different entities in a database.

## ans of 2:-
```sql
USE db2;
CREATE TABLE customers(
cust_id INT(10) NOT NULL,
cust_name VARCHAR(100) NOT NULL,
PRIMARY KEY(cust_id)
);
INSERT INTO customers
VALUES
(1,"Sam Saju"),
(2,"Thoma");

CREATE TABLE orders(
order_id INT(20),
customer_id INT(20),
PRIMARY KEY(order_id),
FOREIGN KEY(customer_id) REFERENCES customers(cust_id)

);
INSERT INTO orders
VALUES
(1001,1),
(1002,2);
SELECT * FROM customers;
SELECT * FROM orders;
```
