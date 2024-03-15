# LEFT JOIN
The LEFT JOIN keyword returns all records from the left table (table1), and the matching records (if any) from the right table (table2).

![image](https://github.com/yadhukishore/EnteSQL/assets/110115711/b29620ba-d563-425d-aa65-40a797841af7)

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

/*Left join*/
SELECT * FROM country LEFT JOIN capital
ON country.co_code = capital.co_code;
```

In the provided SQL script, a `LEFT JOIN` is used to retrieve data from both the `country` and `capital` tables, ensuring that all rows from the `country` table are included in the result set, regardless of whether there is a match in the `capital` table. Here's an explanation of how the `LEFT JOIN` works in this context:

1. **Syntax:**
   ```sql
   SELECT columns
   FROM table1
   LEFT JOIN table2 ON table1.common_column = table2.common_column;
   ```

2. **Explanation:**
   - The `LEFT JOIN` retrieves all rows from the `country` table, and for each row, it attempts to find matching rows in the `capital` table based on the condition specified (`country.co_code = capital.co_code`).
   - If a matching row is found in the `capital` table, the corresponding data from that row is included in the result set.
   - If there is no matching row in the `capital` table for a row in the `country` table, NULL values are used for the columns selected from the `capital` table.
   - In other words, the `LEFT JOIN` ensures that all rows from the left table (`country` table in this case) are included in the result set, regardless of whether there is a matching row in the right table (`capital` table).

3. **Result:**
   The result of the query will include columns from both the `country` and `capital` tables. For rows in the `country` table that have a matching row in the `capital` table based on the `co_code` column, the corresponding data from the `capital` table will be included. For rows in the `country` table that do not have a matching row in the `capital` table, NULL values will be used for the columns selected from the `capital` table.

4. **Example:**
   If we run the provided `LEFT JOIN` query, it will return the following result:
   ```sql
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
   This result shows all countries listed in the `country` table, along with their respective capital cities (`cap_id` and `cap_name`) if available. If a country does not have a corresponding entry in the `capital` table, NULL values are used for the capital-related columns.


