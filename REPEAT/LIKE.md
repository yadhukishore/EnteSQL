Certainly! We can use the `LIKE` operator to perform pattern matching in SQL queries. Here are some examples incorporating `LIKE`:

1. **Retrieve the names and email addresses of employees whose email address contains "example.com":**
```sql
SELECT name, email
FROM employees
WHERE email LIKE '%example.com';
```

2. **List the departments with names starting with "M":**
```sql
SELECT *
FROM departments
WHERE name LIKE 'M%';
```

3. **Find employees whose name starts with "J" and ends with "n":**
```sql
SELECT *
FROM employees
WHERE name LIKE 'J%n';
```

4. **Retrieve employees who joined the company in the year 2010:**
```sql
SELECT *
FROM employees
WHERE hire_date LIKE '2010%';
```

5. **List employees who live in cities starting with "New":**
```sql
SELECT *
FROM employees e
JOIN cities c ON e.city_id = c.id
WHERE c.name LIKE 'New%';
```

These queries use the `LIKE` operator along with wildcard characters `%` to match patterns in the data. `%` represents zero or more characters, so `%example.com` matches any email address ending with "example.com", `M%` matches any department name starting with "M", `J%n` matches names starting with "J" and ending with "n", `2010%` matches any hire date in the year 2010, and `New%` matches any city name starting with "New".
