# Parent-Child Relationship


1. **Parent-Child Relationship:**
   - Imagine you have two tables: `employees` and `departments`. The `departments` table has a primary key `dept_id`, and the `employees` table has a foreign key `dept_id` referencing the `dept_id` in the `departments` table. 
   - Question: How would you ensure that each employee is assigned to an existing department using foreign keys?


```sql
CREATE DATABASE db2;
 CREATE TABLE departments (
 dept_id INT,
 dept_name VARCHAR(50),
 PRIMARY KEY(dept_id)
 );
 INSERT INTO departments
 VALUES
 (1,'Sales'),
 (2,'HR');
 
 CREATE TABLE employees (
 emp_id INT,
 emp_name VARCHAR(60),
 dept_id INT,
 FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
 );
 INSERT INTO employees
 VALUES
 (101,"SAM",1),
 (102,"Yadhu",2);
 
 
 SELECT * FROM departments;
 SELECT * FROM employees;

```

