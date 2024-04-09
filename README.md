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
The SQL JOIN is a command clause that combines records from two or more tables in a database. It is a means of combining data in fields from two tables by using values common to each table. 

 1. **Inner Join:**  An INNER JOIN in SQL is used to retrieve rows from two or more tables based on a related column between them. It returns only the rows where there is a match in both tables, based on the specified join condition.

     - _**Example Tables:**_ <br>
      Table: **employees**

       | id | name    | department_id |
       |----|---------|---------------|
       | 1  | Alice   | 101           |
       | 2  | Bob     | 102           |
       | 3  | Charlie | 103           |
       | 4  | Diana   | 101           |

       Table: **departments** <br>
       
       | id | name       |
       |----|------------|
       | 101| HR         |
       | 102| Marketing  |
       | 103| Finance    |
       | 104| IT         |
       
       <br>
       
       _Example Query:_ Suppose you want to retrieve the names of employees along with the names of their respective departments. You can use an INNER JOIN to achieve this: <br>

       ```sql
       SELECT e.name, d.name as department
       FROM employees e
       INNER JOIN departments d
       ON d.id = e.department_id;
       ```

       This query will return: <br>

       | name    | department |
       |---------|------------|
       | Alice   | HR         |
       | Bob     | Marketing  |
       | Charlie | Finance    |
       | Diana   | HR         |

 2. **LEFT JOIN:**  The LEFT JOIN keyword returns all records from the left table, and the matching records from the right table (table2). The result is 0 records from the right side if there is no match.
    
     - _**Example Tables:**_ <br>
       Table: **students** <br>
    
        | id | name    | age | grade_id |
        |----|---------|-----|----------|
        | 1  | Alice   | 15  | 101      |
        | 2  | Bob     | 16  | 102      |
        | 3  | Charlie | 15  | 101      |
        | 4  | Diana   | 16  | 103      |
        | 5  | Eve     | 15  | NULL     |

       Table: **grades**

       | id  | grade   |
       |-----|---------|
       | 101 | A       |
       | 102 | B       |
       | 103 | C       |


       _Example Query:_ Suppose we want to retrieve all students along with their grades if they have one, using a LEFT JOIN between the students and grades tables.

       ```sql
       SELECT s.name, s.age, g.grade
       FROM students s
       LEFT JOIN grades g
       ON g.id = s.grade_id;
       ```

       This query will return:

       | name    | age | grade |
       |---------|-----|-------|
       | Alice   | 15  | A     |
       | Bob     | 16  | B     |
       | Charlie | 15  | A     |
       | Diana   | 16  | C     |
       | Eve     | 15  | NULL  |
       

       In this query, we are selecting the name and age columns from the students table and the grade column from the grades table. <br>
       
       We're using a LEFT JOIN between the students and grades tables based on the grade_id column in the students table and the id column in the grades table.<br>
       
       The LEFT JOIN includes all rows from the students table regardless of whether there is a matching row in the grades table or not. <br>
       
       If there is a match between the grade_id in the students table and the id in the grades table, the corresponding grade is included in the result.<br>
       
       If there is no match (such as for Eve, whose grade_id is NULL), the grade is shown as NULL in the result.

 3. **RIGHT JOIN:** A RIGHT JOIN is similar to a LEFT JOIN, but it returns all rows from the right table and the matching rows from the left table. In other      words, a RIGHT JOIN retrieves all records from the right table and only the matching records from the left table. If there are no matching records in the left table, NULL values are used for columns from the left table.

     - _**Example Tables:**_ <br>
     
       Table: **orders** <br>

       | order_id | customer_id | product_id | quantity |
       |----------|-------------|------------|----------|
       | 1        | 101         | 201        | 2        |
       | 2        | 102         | 202        | 1        |
       | 3        | 103         | 201        | 3        |
       | 4        | 104         | 203        | 2        |
       | 5        | 105         | 202        | 1        |


       Table: **products** <br>

       | product_id | product_name | price |
       |------------|--------------|-------|
       | 201        | Laptop       | 800   |
       | 202        | Smartphone   | 600   |
       | 203        | Tablet       | 400   |
       | 204        | Headphones   | 100   |

       _Example Query:_ Suppose we want to retrieve all orders along with the product names, using a RIGHT JOIN between the orders and products tables.

       ```sql
       SELECT o.order_id, p.product_name, o.quantity, p.price
       FROM orders o
       RIGHT JOIN products p
       ON p.product_id = o.product_id;
       ```

       This query will return: <br>

       | order_id | product_name | quantity | price |
       |----------|--------------|----------|-------|
       | 1        | Laptop       | 2        | 800   |
       | 2        | Smartphone   | 1        | 600   |
       | 3        | Laptop       | 3        | 800   |
       | 4        | Tablet       | 2        | 400   |
       | 5        | Smartphone   | 1        | 600   |
       | NULL     | Headphones   | NULL     | 100   |

       In this query, we are selecting the order_id from the orders table, product_name from the products table, along with the quantity from the orders table and 
       price from the products table. <br>
       
       We're using a RIGHT JOIN between the orders and products tables based on the product_id column in the orders table and the product_id column in the     
       products table. <br>
       
       The RIGHT JOIN includes all rows from the products table regardless of whether there is a matching row in the orders table or not. <br>

       If there is a match between the product_id in the orders table and the product_id in the products table, the corresponding order information is included in        the result. <br>
       
       If there is no match (such as for the product with ID 204, which has no corresponding record in the orders table), NULL values are used for columns from           the left table (orders).

 4. **FULL OUTER JOIN:** A FULL OUTER JOIN returns all records when there is a match in either the left (first) table or the right (second) table. If there is no match, NULL values are used for the columns from the table that lacks a matching row.

       _**Example Tables:**_

       Table: **employees** <br>
     
       | id | name    | department_id |
       |----|---------|---------------|
       | 1  | Alice   | 101           |
       | 2  | Bob     | 102           |
       | 3  | Charlie | 101           |
       | 4  | Diana   | 103           |


       Table: **departments** <br>

       | id | name       |
       |----|------------|
       | 101| HR         |
       | 102| Marketing  |
       | 103| Finance    |
       | 104| IT         |

       _Example Query:_ Suppose we want to retrieve all employees along with their department names, using a FULL OUTER JOIN between the employees and departments tables.

       ```sql
       SELECT e.name as employee_name, d.name as department_name
       FROM employees e
       FULL OUTER JOIN departments d
       ON d.id = e.department_id
       ```

       This query will return: <br>

       | employee_name | department_name |
       |---------------|-----------------|
       | Alice         | HR              |
       | Bob           | Marketing       |
       | Charlie       | HR              |
       | Diana         | Finance         |
       | NULL          | IT              |

       In this query, we are selecting the name column from the employees table and the name column from the departments table, aliasing them as employee_name and        department_name, respectively. <br>
       
       We're using a FULL OUTER JOIN between the employees and departments tables based on the department_id column in the employees table and the id column in    
       the departments table. <br>
       
       The FULL OUTER JOIN includes all rows from both the employees and departments tables, regardless of whether there is a match in the other table. <br>
       
       If there is a match between the department_id in the employees table and the id in the departments table, the corresponding department name is included in         the result. <br>
       
       If there is no match (such as for the IT department, which has no corresponding employee), NULL values are used for the columns from the table that lacks a        matching row.








