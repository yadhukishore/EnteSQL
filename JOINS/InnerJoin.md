# Inner Join
A JOIN clause is used to combine rows from two or more tables, based on a related column between them.

### if 2 tables having a similar column that matches, each other!

In an SQL `INNER JOIN`, the condition used to join the tables can be based on any column(s) from both tables, not just foreign keys. However, using foreign keys in joins can often simplify the process, especially when the relationship between the tables is well-defined.

Here's an example to illustrate both cases:

1. **Joining on Columns Without Foreign Keys:**
   ```sql
   SELECT *
   FROM table1
   INNER JOIN table2 ON table1.column_name = table2.column_name;
   ```
   In this case, `column_name` from `table1` is being compared to `column_name` from `table2` in the `INNER JOIN` clause. These columns don't necessarily have to be foreign keys, but they should have some relationship that makes sense in the context of the query.

2. **Joining on Foreign Keys:**
   ```sql
   SELECT *
   FROM orders
   INNER JOIN customers ON orders.customer_id = customers.customer_id;
   ```
   Here, `orders.customer_id` is being compared to `customers.customer_id` in the `INNER JOIN` clause. These columns represent a foreign key relationship between the `orders` and `customers` tables. Using foreign keys in joins helps maintain data integrity and makes the query easier to understand, especially in complex databases with multiple tables.

In summary, while it's not strictly necessary for foreign keys to be used in `INNER JOIN` clauses, utilizing them can enhance the clarity and maintainability of your SQL queries, especially when dealing with relationships between tables.

```sql
CREATE DATABASE db2;
USE db2;
CREATE TABLE country(
co_code VARCHAR(10) NOT NULL,
co_name VARCHAR(50),
PRIMARY KEY(co_code)
);
INSERT INTO country
VALUES
('IN','India'),
('UK','United Kingdom'),
('NP','Nepal'),
('PK','Pakisthan'),
('SL','Sri Lanka');
SELECT * FROM country;

CREATE TABLE capital(
cap_id VARCHAR(10) NOT NULL,
co_code VARCHAR(10),
cap_name VARCHAR(100),
PRIMARY KEY(cap_id),
FOREIGN KEY(co_code) REFERENCES country(co_code)
);
INSERT INTO capital
VALUES
('c1','UK','London'),
('c2','IN',"New Delhi"),
('c3','PK','Islamabad');
SELECT * FROM capital;

/*inner join*/
SELECT country.co_code,capital.cap_name FROM country INNER JOIN capital
ON country.co_code = capital.co_code;
```
### OR
```sql
SELECT * FROM country INNER JOIN capital
ON country.co_code = capital.co_code;
```

## Explaination

1. **Syntax:**
   ```sql
   SELECT columns
   FROM table1
   INNER JOIN table2 ON table1.common_column = table2.common_column;
   ```

2. **Explanation:**
   - The `INNER JOIN` combines rows from both `country` and `capital` tables where the `co_code` column from the `country` table matches the `co_code` column from the `capital` table.
   - This condition, `country.co_code = capital.co_code`, establishes the relationship between the two tables.
   - Only rows where the `co_code` value exists in both the `country` and `capital` tables will be included in the result set.

3. **Result:**
   The result of the query will include columns `co_code` from the `country` table and `cap_name` from the `capital` table, where the `co_code` values match between the two tables.

4. **Example:**
   If we run the provided `INNER JOIN` query, it will return the following result:
   ```
   +---------+------------+
   | co_code | cap_name   |
   +---------+------------+
   | IN      | New Delhi  |
   | UK      | London     |
   | PK      | Islamabad  |
   +---------+------------+
   ```
   This result shows the capital cities (`cap_name`) corresponding to the countries (`co_code`) listed in the `country` table, based on the foreign key relationship established between `co_code` in the `country` table and `co_code` in the `capital` table.
