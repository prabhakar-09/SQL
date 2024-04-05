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

--------------------------------------------------------------------

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

**Aggregate Functions**
-----------------------
The _aggregate functions_ are often used to summarize the values of one column with multiple rows into one. In essence, it groups the values of one column into one single value. <br>
These operations are mostly used in conjunction _(in combination)_ with the _GROUP BY Clause_ to perform operations on different rows. Below mentioned are some of the commonly used aggregate functions in SQL.

 1. **COUNT():** is an aggregate function which, simply counts the number of rows in a result set, with or without condition. <br>
    - _Example:_ Consider the below table _students_; <br>
    
      | id | name    | age | gender |
      |----|---------|-----|--------|
      | 1  | Alice   | 20  | Female |
      | 2  | Bob     | 22  | Male   |
      | 3  | Charlie | 21  | Male   |
      | 4  | Diana   | 23  | Female |
      | 5  | Eve     | 20  | Female |

   - Count without condition: Now we're gonna find the number of rows in the _students_ table without any condition. The query would be;

     ```sql
     SELECT COUNT(*) AS total_students
     FROM students
     ```
   - Count with the condition: Now we're going to find the number of female students that exist in the students table. The query would be;
     
     ```sql
     SELECT COUNT(*) AS female_students
     FROM students
     WHERE gender = 'Female'
     ```
We can use the COUNT() function as needed to retrieve data with or without conditions.

 2. **SUM():** is used to sum up all the rows of a specified column and returns one value which is the sum of all the rows. <br>
 
    - _Example:_ Consider the below _sales_ table; <br>
    
      | id | product | quantity | price |
      |----|---------|----------|-------|
      | 1  | Apple   | 10       | 2.5   |
      | 2  | Banana  | 15       | 1.8   |
      | 3  | Orange  | 20       | 2.0   |
      | 4  | Mango   | 12       | 3.5   |
      | 5  | Grape   | 8        | 2.2   |
      
   - Suppose we want to calculate the total revenue generated from the sale, we can simply add up the product of quantity & price to the SUM function. Here's how we can do it; <br>

     ```sql
     SELECT SUM(quantity * price) as total_revenue
     FROM sales;
     ```
   - This query will return the total revenue generated from all sales which is _**149**_
   - This value is calculated by adding up the product of quantity and price for each row in the sales table:
     ```
     Total Revenue = (10 * 2.5) + (15 * 1.8) + (20 * 2.0) + (12 * 3.5) + (8 * 2.2) = 149
     ```
That's how we can use the _SUM()_ function in SQL to calculate the sum of values in a column, which is particularly useful for calculating totals, such as total revenue, total quantity sold, etc. <br>

 3. **AVG():**  is an aggregate function with sums up all the values of the rows of a particular column and divides it by the total number of rows present.

    - _Example:_  Consider the below _sales_ table; <br>
    
      | id | product | quantity | price |
      |----|---------|----------|-------|
      | 1  | Apple   | 10       | 2.5   |
      | 2  | Banana  | 15       | 1.8   |
      | 3  | Orange  | 20       | 2.0   |
      | 4  | Mango   | 12       | 3.5   |
      | 5  | Grape   | 8        | 2.2   |

   - Suppose we need to find the average price of the products which are being sold. The query would be;

      ```sql
      SELECT AVG(price) as average_price
      FROM sales;
      ```
   - This query will return the average price of products sold: **2.4**
   - This value is calculated by summing up all the prices in the price column and then dividing by the total number of rows:
     ```
     Average Price = (2.5 + 1.8 + 2.0 + 3.5 + 2.2) / 5 = 2.4
     ```
That's how you can use the AVG() function in SQL to calculate the average value of a column, which is particularly useful for finding average prices, average quantities, etc.

 4. **MIN():** s an aggregate function used to find the minimum value in a specific column. It returns the smallest value from the set of values in the specified column.

    - _Example:_ Consider the below _sales_ table; <br>

      | id | product | quantity | price |
      |----|---------|----------|-------|
      | 1  | Apple   | 10       | 2.5   |
      | 2  | Banana  | 15       | 1.8   |
      | 3  | Orange  | 20       | 2.0   |
      | 4  | Mango   | 12       | 3.5   |
      | 5  | Grape   | 8        | 2.2   |
      
   - Suppose you want to find the minimum quantity of products sold. You can use the MIN() function to find the smallest quantity:

     ```sql
     SELECT MIN(quantity) as minimum_quantity
     FROM sales;
     ```
   - The above query will return the minimal numeral from the table for a specific column which is 8. <br>
   
That's how you can use the MIN() function in SQL to find the minimum value of a column, which is particularly useful for identifying the lowest quantity, lowest price, etc.

 5. **MAX():** is an aggregate function used to find the maximum value in a specific column. It returns the largest value from the set of values in the specified column.

    - _Example:_ Consider the below _sales_ table; <br>

      | id | product | quantity | price |
      |----|---------|----------|-------|
      | 1  | Apple   | 10       | 2.5   |
      | 2  | Banana  | 15       | 1.8   |
      | 3  | Orange  | 20       | 2.0   |
      | 4  | Mango   | 12       | 3.5   |
      | 5  | Grape   | 8        | 2.2   |

   - Suppose you want to find the maximum quantity of products sold. You can use the MAX() function to find the largest quantity:

     ```sql
     SELECT MAX(quantity) AS max_quantity
     FROM sales;
     ```
   - The above query will return the maximum number(the quantity) from the quantity column which is 20. <br>
   
That's how you can use the MAX() function in SQL to find the maximum value of a column, which is particularly useful for identifying the highest quantity, highest price, etc.
<br>

**JOINS**
----------------------------------
