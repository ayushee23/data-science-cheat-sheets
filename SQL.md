# SQL Cheat Sheet

This sheet contains common SQL concepts, commands, and best practices that I encountered while studying

- Database is a collection of tables

- Schema is a blueprint which tells how the data is organized within a database - what tables are there, columns for each table, data types for each column, how tables are related, and any rules such as primary/foreign key constraints

- Comparison operators (=, !, >, <) can be used on both numerical and non-numerical data. With non-numerical data, the value beimg compared should be in single quotes. 

- Logical operators - LIKE, IN, BETWEEN, AND, OR, NOT, IS NULL
    - Wildcards are used with LIKE (% matches a single or set of characters, _ matches a single character)
    - LIKE is case-sensitive, ILIKE is case-insensitive
    - BETWEEN includes range bounds
    - IS NULL is used to filter out null values (column=NULL doesn't work as you can't perform arithmetic operatiosn on NULL values)
    - NOT is generally used with LIKE, NULL
    - Arithmetic operators such as col_name!=2 will leave out NULL values as comparison with NULL values returns unknown which is treated as FALSE, so if the result set should include these values put an additional filter (col_name IS NULL) to include them or use COALESCE(col_name, 0) to treat NULL like a real value
 
- CHAR_LENGTH() Vs LENGTH() // char_length() returns length of string measured in number of characters and length() returns length of string measured in bytes

- Aggregate Functions (only aggregate vertically; for horizontal calculations arithmetic operators are used)
    - COUNT is used to count the number of non-null rows
    - SUM treats NULLs as 0
    - MIN/MAX ignores NULLs
    - AVG ignores NULLs; in cases where you want to include those convert NULL to real value (0) using COALESCE
 
- Aggregate functions aggregate across whole table but in cases where we want to aggregate a certain part/group of the table GROUP BY is used. GROUP BY allows you to divide data into groups and perform operations on groups




- CASE statements are used to handle IF/ELSE situations. A CASE statement will have at least 1 WHEN/THEN and ends with END. ELSE is optional.
- Aggregation of CASE statements is done to pivot data horizontally
- Using DISTINCT, particularly in aggregations, can slow your queries down quite a bit

  Window functions (https://www.youtube.com/watch?v=bi2qAVeSpBM&list=PLbTF1OfX62c3RQ_ZFfyNBWVPdz_OWTMLG)



  Data Warehouse Modeling(https://www.youtube.com/watch?v=g-FCc-NHOsg&list=PLTsNSGeIpGnGP8A74Ie1PgqHhewsqD3fv&index=2)

  
  Database(MySQL, Postgres, oracle) Vs Data Warehouse(teradata, exadata, redshift, snowflake)

  Data warehouse is built on top of database(made from multiple databases) but used for different purposes. DW handles larges amounts of data, has read-heavy operations, optimal for high-latency operations, contains denormalized data(can contain redundant data), columnar storage(parquet), optimized for parallel processing, OLAP systems use data warehousing solutions. DW solutions work mostly on structured data(as opposed to Spark). DW integrates data coming from multiple sources. 
  
  Database is designed to store small amounts of data, for write-heavy operations, used for low-latency operations, normalized data, row-based storage, not optimized for parallel processing, OLTP use database solutions

  In DW, we do ETL(Extract data from sources, transform the data and load into data warehouse/databases). Problem with this is - the rate at which big data is generated(3V's) this can't transform it with that speed and with this we also have to know the transformations that have to be applied to data beforehand(requires pre-defined schema), can handle only structured data, and is expensive as data processing and storage needs increase and due to vertical scaling it can be scaled only to a certain point. This is where data lake comes into picture.



  Data lake(s3 bucket, azure blob, HDFS) - lets you load all of the data into data storage and transform it on need basis; u nlimited storage due to horizontal scaling. It supports structured, semi-struc, unstructured data.

  In intial data lake systems, you could just use it for data storage and then pass it to data warehouse for transformation. But now data lake systems have become refined and they can handle transformations as well. They consist of 4 layers -
  Ingestion layer - raw data storage
  Processing - process the data
  Processed - processed data based on use case(enginner level data access)
  Consumption - business users/reporting tools take data from this layer(business users data access). At this stage, data could also be sent to a database/data warehouse(optional)



Data Mart - can be considered a subset of data warehouse containing data for a specific purpose. Data from different departments/demographics/regions is fetched from DW and put into data marts through ETL. Useful for business users who want only relevant data, or summarized tables and enables faster query performance. It also protects data about different departments or other important data from unwanted access. 





Spark(https://www.youtube.com/watch?v=_piYXmAXHW8&list=PLkz1SCf5iB4dXiPdFD4hXwheRGRwhmd6K&index=3)



Spark is Hadoop successor(HDFS, MapReduce, YARN) -- MapReduce was difficult to code and not that great so Spark came(developed by UC Berkeley). Spark is used for handling and processing big data through a cluster of computers. Spark is a processing engine and doesn't come with storage system(HDFS, S3, Google Cloud, Cassandra) and cluster manager(YARN, Kubernetes). You can use any of the others for storage and cluster management. 
Spark Core(heart of Spark) - computing engine + core APIs
Computing engine does memory management, task scheduling, fault recovery, interacting with cluster manager
Core APIs - structured(optimized to handle dataframes, datasets) and unstructured APIs(low-level APIs like RDDs, accumulator, broadcast variables)

Outside of Spark Core we have 4 sets of libraries and packages - Spark SQL(allows to use SQL for structured data), Streaming(to process continuous data streams), MLlib(machine learning libraries), GraphX(contains libs of graph algorithms). They all depend on Spark Core for distributed data processing. 

What makes Spark great? abstracts away the fact that you are coding to execute on a cluster of computers, abstracts away complexities of distributed storage, resource management and parallel processing













. What is SQL, and why is it used?SQL (Structured Query Language) is a standard programming language used to manage and manipulate relational databases. It is used for querying, updating, inserting, and deleting data, as well as for creating and managing database structures.

2. What are the different types of SQL statements?

DDL (Data Definition Language): CREATE, ALTER, DROP — define and modify database structure.

DML (Data Manipulation Language): SELECT, INSERT, UPDATE, DELETE — manage data.

DCL (Data Control Language): GRANT, REVOKE — manage permissions.

TCL (Transaction Control Language): COMMIT, ROLLBACK, SAVEPOINT — control transactions.

3. What are primary keys and foreign keys?

Primary Key: A column or set of columns that uniquely identifies each row in a table.

Foreign Key: A column that creates a relationship between two tables by referencing a primary key in another table.

4. Explain the difference between WHERE and HAVING clauses.

WHERE filters rows before grouping.

HAVING filters groups after aggregation.

5. What are SQL constraints? Name and explain the common ones.Constraints ensure data integrity:

NOT NULL: Prevents NULL values.

UNIQUE: Ensures all values are unique.

PRIMARY KEY: Combines NOT NULL and UNIQUE.

FOREIGN KEY: Enforces relationships.

CHECK: Ensures a condition is met.

DEFAULT: Sets a default value.

6. Explain the difference between INNER JOIN and OUTER JOIN.

INNER JOIN: Returns only matching rows.

OUTER JOIN: Returns all rows from one or both tables, with NULLs where there are no matches.

7. What is a NULL value in SQL, and how do you handle it?NULL represents missing or unknown data. Use IS NULL or IS NOT NULL to filter, and functions like COALESCE or IFNULL to replace.

8. What is the difference between DISTINCT and GROUP BY?

DISTINCT: Removes duplicate rows.

GROUP BY: Groups rows to apply aggregate functions.

9. What is a UNION in SQL, and how is it different from UNION ALL?

UNION: Combines results of two queries and removes duplicates.

UNION ALL: Combines all results, including duplicates.

Intermediate

1. What is a subquery, and how is it used?A subquery is a query inside another query. It can return single or multiple values used in WHERE, FROM, or SELECT clauses.

2. Explain the difference between correlated and non-correlated subqueries.

Correlated: Depends on the outer query; runs row-by-row.

Non-correlated: Runs independently of the outer query.

3. How do you use CASE statements with aggregation in SQL?Use CASE within aggregate functions to perform conditional counts/sums.Example:

SELECT department, SUM(CASE WHEN gender = 'F' THEN 1 ELSE 0 END) AS female_count FROM employees GROUP BY department;

4. How do you use window functions in SQL?Window functions perform calculations across a set of rows related to the current row. Examples include RANK(), ROW_NUMBER(), LEAD(), LAG().

5. What are stored procedures, and how do you create one?Stored procedures are saved SQL code that can be reused.Example:

CREATE PROCEDURE GetEmployees AS BEGIN SELECT * FROM employees; END;

6. What is a trigger, and when would you use it?A trigger automatically runs in response to specific events (e.g., INSERT, UPDATE) on a table. Used for enforcing business rules.

7. How do you use the GROUP_CONCAT function?GROUP_CONCAT combines values from multiple rows into a single string (available in MySQL).

SELECT department, GROUP_CONCAT(name) FROM employees GROUP BY department;

8. Explain the purpose of the COALESCE function.COALESCE returns the first non-NULL value in a list. Used for handling NULLs.

9. How do you use the RANK and DENSE_RANK functions?Used with OVER(ORDER BY ...) to assign rankings.

RANK() can skip numbers.

DENSE_RANK() does not skip ranks.

10. What are SQL transactions, and how do you manage them?Transactions are sequences of operations treated as a single unit. Use BEGIN, COMMIT, and ROLLBACK to control them.

11. Explain isolation levels in SQL and their importance.Isolation levels define how transactions interact:

Read Uncommitted: Can see uncommitted changes.

Read Committed: Only sees committed data.

Repeatable Read: Same results if reread.

Serializable: Highest level, full isolation.

Advanced

1. How do you optimize a slow SQL query?Use indexing, avoid SELECT *, reduce joins, use WHERE clauses, analyze execution plans.

2. Explain the concept of database normalization.Organizing data to reduce redundancy. Normal forms (1NF, 2NF, 3NF) help structure data efficiently.

3. What is denormalization, and when would you use it?Combining tables to reduce joins and improve performance, especially in read-heavy systems.

4. What are materialized views, and how do they differ from standard views?Materialized views store data physically, unlike standard views which are virtual. Used to improve query performance.

5. How do you implement recursive queries in SQL?Use Common Table Expressions (CTEs) with recursion.Example:

WITH RECURSIVE emp_cte AS (
  SELECT id, manager_id, name FROM employees WHERE manager_id IS NULL
  UNION ALL
  SELECT e.id, e.manager_id, e.name FROM employees e
  JOIN emp_cte c ON e.manager_id = c.id
) SELECT * FROM emp_cte;

6. What is partitioning in SQL, and how is it useful?Partitioning splits tables into smaller parts to improve performance and manageability. Types: range, list, hash, composite.

7. How do you analyze a query execution plan?Use EXPLAIN or EXPLAIN ANALYZE to understand how queries run—check for full table scans, indexes used, and join strategies.

8. What are common table expressions (CTEs), and how do you use them?CTEs are temporary result sets used to simplify complex queries. Written using WITH clause.

9. How do you design a database schema for scalability?Use normalization, indexing, proper data types, avoid bottlenecks, plan for sharding or replication if needed.

10. What is the difference between OLTP and OLAP databases?

OLTP (Online Transaction Processing): Handles real-time transactions, optimized for speed and reliability.

OLAP (Online Analytical Processing): Used for data analysis and reporting, optimized for complex queries and aggregation.




