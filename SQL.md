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

