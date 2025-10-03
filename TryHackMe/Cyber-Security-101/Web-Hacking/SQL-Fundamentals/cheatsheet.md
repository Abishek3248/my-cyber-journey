# Cheatsheet - SQL Fundamentals

| Category                | Command / Function / Clause                     | Description / Usage Example                                                                                   |
|-------------------------|------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| **Database Statements** | CREATE DATABASE db_name;                        | Creates a new database                                                                                         |
|                         | SHOW DATABASES;                                 | Lists all databases                                                                                             |
|                         | USE db_name;                                    | Selects a database to use                                                                                      |
|                         | DROP DATABASE db_name;                          | Deletes a database                                                                                              |
| **Table Statements**    | CREATE TABLE table_name (columns...);           | Creates a new table with specified columns and data types                                                      |
|                         | SHOW TABLES;                                    | Lists tables in current database                                                                                |
|                         | DESCRIBE table_name;                            | Shows column structure of a table                                                                              |
|                         | ALTER TABLE table_name ADD column_name type;    | Adds a new column                                                                                               |
|                         | DROP TABLE table_name;                           | Deletes a table                                                                                                 |
| **CRUD Operations**     | INSERT INTO table_name (columns) VALUES (...); | Adds a new record                                                                                               |
|                         | SELECT * FROM table_name;                        | Retrieves all records                                                                                           |
|                         | SELECT column1, column2 FROM table_name;       | Retrieves specific columns                                                                                      |
|                         | UPDATE table_name SET column=value WHERE ...;  | Updates existing records                                                                                         |
|                         | DELETE FROM table_name WHERE ...;              | Deletes records                                                                                                 |
| **Clauses**             | DISTINCT                                       | Returns only unique values                                                                                       |
|                         | GROUP BY column                                 | Groups results for aggregation                                                                                  |
|                         | ORDER BY column ASC|DESC                        | Sorts results in ascending or descending order                                                                 |
|                         | HAVING condition                                | Filters results after aggregation                                                                               |
| **Logical Operators**   | AND                                            | Both conditions must be true                                                                                     |
|                         | OR                                             | At least one condition must be true                                                                              |
|                         | NOT                                            | Reverses condition                                                                                               |
| **Comparison Operators**| =, !=, <, >, <=, >=                             | Checks equality, inequality, greater/less than, or range                                                      |
|                         | BETWEEN value1 AND value2                       | Checks if value is within a range                                                                               |
|                         | LIKE '%pattern%'                                | Pattern matching                                                                                                 |
| **String Functions**    | CONCAT(str1, str2, ...)                         | Combines strings                                                                                                |
|                         | GROUP_CONCAT(column SEPARATOR ', ')            | Concatenates multiple row values into a single string                                                         |
|                         | SUBSTRING(column, start, length)               | Extracts part of a string                                                                                        |
|                         | LENGTH(column)                                  | Returns string length                                                                                            |
| **Aggregate Functions** | COUNT(column)                                   | Counts number of rows                                                                                             |
|                         | SUM(column)                                     | Sums numeric column                                                                                               |
|                         | MAX(column)                                     | Returns maximum value                                                                                            |
|                         | MIN(column)                                     | Returns minimum value                                                                                            |
