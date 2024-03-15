# Cross Join
- The CROSS JOIN keyword returns all records from both tables (table1 and table2).
- CROSS JOIN can potentially return very large result-sets!


![image](https://github.com/yadhukishore/EnteSQL/assets/110115711/be901e8e-f086-42a8-bc8b-8ddc448e1651)
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

/*Cross join*/
SELECT * FROM country CROSS JOIN capital;



```



In the provided SQL script, a `CROSS JOIN` is used to retrieve data from both the `country` and `capital` tables by combining each row from the `country` table with every row from the `capital` table. Here's an explanation of how the `CROSS JOIN` works in this context:

1. **Syntax:**
   ```sql
   SELECT columns
   FROM table1
   CROSS JOIN table2;
   ```

2. **Explanation:**
   - The `CROSS JOIN` returns the Cartesian product of the two tables involved, meaning it combines each row from the first table (`country` table) with every row from the second table (`capital` table).
   - Unlike other types of joins, the `CROSS JOIN` does not have an `ON` condition to specify how the tables should be joined. Instead, it simply combines all rows from both tables, creating a result set with every possible combination of rows.
   - The number of rows in the result set produced by a `CROSS JOIN` is equal to the product of the number of rows in each table. For example, if the `country` table has `n` rows and the `capital` table has `m` rows, the result will have `n * m` rows.
   - The `CROSS JOIN` can be memory-intensive and can quickly generate large result sets, especially when used with tables that contain a large number of rows.

3. **Result:**
   The result of the `CROSS JOIN` query will include all columns from both the `country` and `capital` tables, with each row from the `country` table combined with every row from the `capital` table.

4. **Example:**
   If we run the provided `CROSS JOIN` query, it will return the Cartesian product of the `country` and `capital` tables, resulting in a combination of every country-capital pair:
   ```
   +---------+------------+--------+------------+
   | co_code | co_name    | cap_id | cap_name   |
   +---------+------------+--------+------------+
   | IN      | India      | c1     | London     |
   | IN      | India      | c2     | New Delhi  |
   | IN      | India      | c3     | Islamabad  |
   | UK      | United...  | c1     | London     |
   | UK      | United...  | c2     | New Delhi  |
   | UK      | United...  | c3     | Islamabad  |
   | NP      | Nepal      | c1     | London     |
   | NP      | Nepal      | c2     | New Delhi  |
   | NP      | Nepal      | c3     | Islamabad  |
   | PK      | Pakisthan  | c1     | London     |
   | PK      | Pakisthan  | c2     | New Delhi  |
   | PK      | Pakisthan  | c3     | Islamabad  |
   | SL      | Sri Lanka  | c1     | London     |
   | SL      | Sri Lanka  | c2     | New Delhi  |
   | SL      | Sri Lanka  | c3     | Islamabad  |
   +---------+------------+--------+------------+
   ```
   As shown, each country-capital combination is listed, resulting in a total of `5 (countries) * 3 (capitals)` = `15` rows in the result set.

