# 175. Combine Two Tables


Table: Person

```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| personId    | int     |
| lastName    | varchar |
| firstName   | varchar |
+-------------+---------+
```
`personId` is the primary key (column with unique values) for this table.


This table contains information about the ID of some persons and their first and last names.
 

Table: Address
```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| addressId   | int     |
| personId    | int     |
| city        | varchar |
| state       | varchar |
+-------------+---------+
```
`addressId` is the primary key (column with unique values) for this table.

Each row of this table contains information about the city and state of one person with `ID = PersonId`.
 

Write a solution to report the first name, last name, city, and state of each person in the Person table. If the address of a personId is not present in the Address table, report null instead.

Return the result table in any order.


### To solve this problem, you can use a `LEFT JOIN` between the `Person` table and the `Address` table on the `personId` column. This will ensure that all rows from the `Person` table are included in the result, and if there is a matching row in the `Address` table, the city and state information will be retrieved. If there is no matching row in the `Address` table for a personId, NULL values will be used for the city and state columns.

Here's the SQL query to achieve this:

```sql
SELECT 
    p.firstName,
    p.lastName,
    a.city,
    a.state
FROM 
    Person p
LEFT JOIN 
    Address a 
ON 
    p.personId = a.personId;
```

This query selects the first name and last name from the `Person` table and the city and state from the `Address` table, ensuring that all rows from the `Person` table are included. If there is no corresponding address for a personId in the `Address` table, NULL values will be returned for the city and state.
