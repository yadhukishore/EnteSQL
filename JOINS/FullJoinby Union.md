# Full Join

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

/*Full join*/
SELECT * FROM country LEFT JOIN capital
ON country.co_code = capital.co_code
UNION
SELECT * FROM country RIGHT JOIN capital
ON country.co_code = capital.co_code;
```

In the provided SQL script, a `FULL JOIN` (also known as a `FULL OUTER JOIN`) is used to combine the results of both `LEFT JOIN` and `RIGHT JOIN`. Here's an explanation of how the `FULL JOIN` works in this context:

1. **Syntax:**
   ```sql
   SELECT columns
   FROM table1
   LEFT JOIN table2 ON table1.common_column = table2.common_column
   UNION
   SELECT columns
   FROM table1
   RIGHT JOIN table2 ON table1.common_column = table2.common_column;
   ```

2. **Explanation:**
   - The `FULL JOIN` retrieves all rows from both the `country` and `capital` tables. It attempts to match rows from both tables based on the condition specified (`country.co_code = capital.co_code`).
   - If a matching row is found in both tables, the corresponding data from both tables is included in the result set.
   - If a row exists in one table but not in the other, NULL values are used for the columns from the table that does not have a matching row.
   - In other words, the `FULL JOIN` ensures that all rows from both tables are included in the result set, regardless of whether there is a matching row in the other table.

3. **Result:**
   The result of the query will include columns from both the `country` and `capital` tables. For rows in the `country` table that have a matching row in the `capital` table based on the `co_code` column, the corresponding data from the `capital` table will be included. For rows in the `capital` table that do not have a matching row in the `country` table, NULL values will be used for the country-related columns, and vice versa.

4. **Example:**
   If we run the provided `FULL JOIN` query, it will return the following result:
   ```
   +---------+------------+--------+------------+
   | co_code | co_name    | cap_id | cap_name   |
   +---------+------------+--------+------------+
   | IN      | India      | c2     | New Delhi  |
   | UK      | United...  | c1     | London     |
   | NP      | Nepal      | NULL   | NULL       |
   | PK      | Pakisthan  | c3     | Islamabad  |
   | SL      | Sri Lanka  | NULL   | NULL       |
   +---------+------------+--------+------------+
   ```
   This result shows all countries listed in the `country` table, along with their respective capital cities (`cap_id` and `cap_name`) if available. If a country does not have a corresponding entry in the `capital` table, NULL values are used for the capital-related columns, and vice versa.
