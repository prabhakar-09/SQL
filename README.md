# SQL

 List of SQL topics ranging from basic to advanced levels:

Basic SQL Queries:

  - SELECT statement
  - WHERE clause
  - ORDER BY clause
  - LIMIT and OFFSET
  - Aggregate functions (COUNT, SUM, AVG, MIN, MAX)

Joins:

  - INNER JOIN
  - LEFT JOIN
  - RIGHT JOIN
  - FULL OUTER JOIN
  - CROSS JOIN
  
Subqueries:

  - Single-row subqueries
  - Multi-row subqueries
  - Correlated subqueries
  
Advanced Filtering:

  - IN operator
  - BETWEEN operator
  - LIKE operator
  - IS NULL and IS NOT NULL
  
Grouping and Aggregation:

  - GROUP BY clause
  - HAVING clause
  - Grouping sets, rollup, and cube
  
Set Operations:

  - UNION
  - UNION ALL
  - INTERSECT
  - EXCEPT
  
Modifying Data:

  I- NSERT statement
  - UPDATE statement
  - DELETE statement
  - Transactions and ACID properties
  
Indexes and Performance Tuning:

  - Understanding indexes
  - Creating indexes
  - Query optimization techniques
  - Analyzing query performance
  
Advanced SQL Techniques:

  - Common Table Expressions (CTEs)
  - Window Functions
  - Recursive Queries
  - Pivoting and Unpivoting data
  
Stored Procedures, Functions, and Triggers:

  - Creating stored procedures
  - Creating user-defined functions
  - Implementing triggers
  - Handling exceptions and errors
  
Advanced Data Modeling:

  - Normalization
  - Denormalization
  - Entity-Relationship Modeling (ERD)
  - Data warehousing concepts
  
Advanced Topics:



  - Working with JSON data
  - Working with XML data
  - Geospatial data handling
  - Security and permissions management

##########################################################################################

**THE SELECT STATEMENT**
--------------------------

  - The SELECT statement in SQL is used to retrieve data from a database. It's the most commonly used SQL command and follows this basic syntax:
  
  ``` sql
  SELECT column1, column2, ...
  FROM table_name
  WHERE condition;
  ```
   SELECT: Specifies the columns you want to retrieve. <br>
   FROM: Specifies the table from which to retrieve the data. <br>
   WHERE: Optional; filters the rows returned based on specified conditions. <br>
  
 ``` sql 
 SELECT name, age FROM employees;
 ```

This will return only the "name" and "age" columns for all rows in the "employees" table. 

**ORDER BY Clause**
---------------------
- The ORDER BY clause is used to sort the result set returned by a SQL query in ascending or descending order based on one or more columns. By default, the sorting is done in ascending order. You can specify the   column(s) by which you want to sort, and optionally specify the direction of sorting (ascending or descending) using the ASC or DESC keywords respectively.
- _Example :_ Consider a table named students with columns id, name, and age. If you want to retrieve the names of students sorted alphabetically in ascending order, you can use the ORDER BY clause as follows:

```sql
SELECT name
FROM students
ORDER BY name ASC;
```
- _Example Query:_
Now, let's combine the SELECT statement, WHERE clause, and ORDER BY clause into a single example query:
Suppose you want to retrieve the names and ages of students who are older than 20 years, sorted by their ages in descending order. You can use the following query:

```sql
SELECT name, age
FROM students
WHERE age > 20
ORDER BY age DESC;
```
This query will first filter the rows from the students table where the age is greater than 20, then it will retrieve the names and ages of those students, and finally, it will sort the result set based on the age column in descending order.

**LIMIT Clause**
------------------

- The _LIMIT_ Clause is used to restrict the number of rows retrieved by the Query.
- It's often used in combination with the _SELECT_ Statement to set a limit on the number of rows the query returns.
- _Example:_ Suppose we've a table _employees_ and we want to retrieve only first 10 records from the table. Here's how we're gonna do it;

  ```sql
  SELECT * FROM employees
  LIMIT 10;
  ```
This query will return only the first 5 rows from the employees table.


**OFFSET Clause**
--------------------
- The _OFFSET_ Clause is used to skip specified number of rows before starting to fetch the result set.
- It's often used in combination with _LIMIT_ Clause to implement pagination or skip certain number of rows while fetching records from DB.
- _Example:_ Suppose you want to retrieve next 5 or 10 rows after skipping first five rows. Here's how we're gonna do it;

  ``` sql
  SELECT * FROM employees
  LIMIT 5 OFFSET 5;
  ```
  This query will skip the first 5 rows and return the next 5 rows from the employees table.
  
LIMIT and OFFSET are simple yet powerful clauses used to control the number of rows returned by a query and to skip rows when necessary.
