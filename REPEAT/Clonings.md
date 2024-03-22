SQL Cloning Operation allows to create the exact copy of an existing table along with its definition. There are three types of cloning possible using SQL in various RDBMS; they are listed below −

- Simple Cloning
- Shallow Cloning
- Deep Cloning
  # Simple Cloning in MySQL



Simple cloning operation creates a new replica table from the existing table and copies all the records in newly created table. To break this process down, a new table is created using the CREATE TABLE statement; and the data from the existing table, as a result of SELECT statement, is copied into the new table.

Here, clone table inherits only the basic column definitions like the NULL settings and default values from the original table. It does not inherit the indices and AUTO_INCREMENT definitions.

Syntax
Following is the basic syntax to perform simple cloning in MySQL−

```SQL
CREATE TABLE new_table SELECT * FROM original_table;
```
## Shallow Cloning 
Cloning using `LIKE` typically refers to creating a new database object that is similar to an existing one by using a pattern matching approach to copy certain properties or attributes.

For example, let's say you have a table named `employees` in your database, and you want to create a new table named `employees_backup` that contains only the employees whose names start with "A". You can use `LIKE` to specify a pattern for the names and then copy the matching rows into the new table.

Here's an example SQL query to achieve this:

```sql
CREATE TABLE employees_backup AS
SELECT *
FROM employees
WHERE name LIKE 'A%';
```

In this query:
- `employees_backup` is the new table being created.
- `employees` is the existing table from which data is being copied.
- `WHERE name LIKE 'A%'` specifies that only rows where the `name` column starts with "A" will be copied to the new table.

This creates a clone of the `employees` table, but only includes the rows that match the specified pattern in the `name` column. The `LIKE` operator is used here to define the pattern for selecting rows to be copied.

