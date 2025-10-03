# SQL Fundamentals

## Introduction
- Cyber security is a broad topic that covers a wide range of subjects, but few of those are as ubiquitous as databases. Whether you’re working on securing a web application, working in a SOC and using a SIEM, configuring user authentication/access control, or using malware analysis/threat detection tools (the list goes on), you will in some way be relying on databases. For example, on the offensive side of security, it can help us better understand SQL vulnerabilities, such as SQL injections, and create queries that help us tamper or retrieve data within a compromised service. On the other hand, on the defensive side, it can help us navigate through databases and find suspicious activity or relevant information; it can also help us better protect a service by implementing restrictions when needed.


## Databases

### Concepts Learned
- Databases are organized collections of structured information, used widely in almost all modern systems.
- Two main types of databases: Relational (SQL) and Non-relational (NoSQL).
- Relational databases store data in tables, rows, and columns.
- Non-relational databases store data in non-tabular formats (documents, key-value pairs, collections).
- Relational DBs require data types (String, Integer, Float/Decimal, Date/Time).
- Relationships between tables are maintained using Primary Keys and Foreign Keys.

### Explanation
**Databases**
  - Organized collections of structured data that can be easily accessed, manipulated, and analyzed.
**Examples:**
  - User authentication data (usernames, passwords).
  - Social media data (posts, comments, likes).
  - Streaming service data (watch history, recommendations).
**Types of Databases**
**Relational Databases (SQL):**
  - Store structured data in tables (rows & columns).
  - Relationships can be created between tables.
  - Example: users and order_history tables linked by user ID.
**Non-relational Databases (NoSQL):**
  - Store data in flexible, unstructured formats.
  - Examples: JSON-like documents, key-value stores.
  - Good for scenarios with varying data formats, like social media.
  - Tables, Rows, and Columns (Relational Databases)
  - Table: Collection of related data (e.g., Books).
  - Columns: Define attributes of the data (e.g., id, Name, Published_date).
  - Rows: Individual records (e.g., book entry with ID=1, Name="Android Security Internals").
**Data Types:**
  - String → text data
  - Integer → whole numbers
  - Float/Decimal → numbers with decimals
  - Date/Time → temporal values
**Keys in Databases**
**Primary Key:**
  - Unique identifier for each record in a table.
  - Example: id in the Books table.
  - Only one per table.
**Foreign Key:**
  - A column in one table that refers to the Primary Key in another.
  - Establishes relationships between tables.
  - Example: author_id in Books table referencing id in Authors table.

### Notes
- Databases are everywhere → from small businesses to massive enterprises.
- Relational DBs (SQL) → structured, consistent, accurate (e.g., e-commerce transactions).
- Non-relational DBs (NoSQL) → flexible, scalable, better for unstructured/varying data (e.g., social media).
- Tables = structured data storage.
- Primary Key = uniqueness.
- Foreign Key = relationships.


## SQL

### Concepts Learned
- DBMS (Database Management System) serves as an interface between users and the database (examples: MySQL, MongoDB, Oracle DB, MariaDB).
- SQL (Structured Query Language) is used to interact with relational databases.
- SQL can query, define, and manipulate relational data.
- Benefits of SQL & Relational Databases: Fast, Easy to Learn, Reliable, Flexible.
- Hands-on SQL starts with connecting to MySQL via terminal commands.

### Explanation
- DBMS is a software layer between the end user and the database,That Allows data retrieval, updates, and management.
**examples:**
  - MySQL → widely used open-source relational DBMS.
  - MongoDB → non-relational (NoSQL).
  - Oracle DB → enterprise-grade RDBMS.
  - MariaDB → MySQL fork, community-driven.
- Structured Query Language (SQL) is the standard language for managing relational databases.
**Core functions:**
  - Querying data (SELECT).
  - Defining database structures (CREATE).
  - Manipulating data (INSERT, UPDATE, DELETE).
**Benefits**
  - Fast: Optimized to handle large datasets quickly.
  - Easy to Learn: Uses plain-English-like syntax.
  - Example: SELECT name FROM users;
  - Reliable: Enforces structured data formats, ensuring consistency.
  - Flexible: Wide range of queries and operations for analysis and reporting.
**Getting Hands-On with SQL**
  - *Start a MySQL session:*
    - mysql -u root -p
  - *Enter the password:*
    - tryhackme
  - From here, SQL queries can be executed (e.g., SHOW DATABASES;).

### Notes
- DBMS = bridge between user and database.
- SQL = language to communicate with relational DBs.
- Relational DBs + SQL = fast, accurate, flexible data management.
- SQL syntax is readable and beginner-friendly compared to other programming languages.


## Database and Table Statements

### Concepts Learned
- SQL statements for databases: CREATE DATABASE, SHOW DATABASES, USE, DROP DATABASE.
- SQL statements for tables: CREATE TABLE, SHOW TABLES, DESCRIBE, ALTER, DROP TABLE.
- Understanding data types, constraints, and keys (e.g., INT, VARCHAR, DATE, NOT NULL, PRIMARY KEY).
- Managing database schema through create, list, modify, and delete operations.

### Explanation
**Database Statements**
**CREATE DATABASE:**
  - CREATE DATABASE thm_bookmarket_db;
  - Creates a new database.
**SHOW DATABASES:**
  - SHOW DATABASES;
  - Lists all databases, including system databases like mysql, information_schema, performance_schema, and sys.
**USE DATABASE:**
  - USE thm_bookmarket_db;
  - Selects a database as the active one for subsequent queries.
**DROP DATABASE:**
  - DROP DATABASE database_name;
  - Deletes a database permanently.
**Table Statements**
**CREATE TABLE:**
  - "CREATE TABLE book_inventory (
    book_id INT AUTO_INCREMENT PRIMARY KEY,
    book_name VARCHAR(255) NOT NULL,
    publication_date DATE
);"
  - book_id: Integer, auto-incremented, primary key.
  - book_name: Text field (max 255 chars), cannot be empty (NOT NULL).
  - publication_date: Stores dates (YYYY-MM-DD format).
**SHOW TABLES:**
  - SHOW TABLES;
  - Lists all tables in the currently active database.
**DESCRIBE (DESC):**
  - DESCRIBE book_inventory;
  - Displays table schema (column names, types, keys, nullability, defaults).
**ALTER TABLE:**
  - ALTER TABLE book_inventory
  - ADD page_count INT;
  - Modifies an existing table (e.g., add/remove columns, change data type, rename).
**DROP TABLE:**
  - DROP TABLE table_name;
  - Permanently deletes a table.

### Notes
- Databases hold collections of tables.
- Tables hold rows (records) and columns (fields).
- Every table must have a Primary Key (unique identifier).
**Data Types (commonly used):**
  - INT → whole numbers.
  - VARCHAR(n) → text up to n characters.
  - DATE → date values.
**Constraints improve data integrity:**
  - NOT NULL → field cannot be empty.
  - AUTO_INCREMENT → automatically increments numeric values.
  - PRIMARY KEY → uniquely identifies rows.
- Use ALTER to evolve schema when business needs change.
- Use DROP with caution (both databases & tables).


## CRUD Operations

### Concepts Learned
- CRUD = Create, Read, Update, Delete → the 4 core operations for managing data in relational databases.
**SQL statements for CRUD:**
  - INSERT INTO → Add new records.
  - SELECT → Retrieve records.
  - UPDATE → Modify existing records.
  - DELETE → Remove records.
  - Importance of the WHERE clause in UPDATE and DELETE to avoid changing/deleting all rows.

### Explanation
**Create (INSERT INTO)**
  - Used to add new rows to a table.
  - INSERT INTO books (id, name, published_date, description)
    VALUES (1, "Android Security Internals", "2014-10-14", 
             "An In-Depth Guide to Android's Security Architecture");
  - Adds a record with specified values for each column.
  - If no column list is specified, values must match table definition order.
**Read (SELECT)**
  - Used to retrieve records.
**Select all columns:**
  - SELECT * FROM books;
**Select specific columns:**
  - SELECT name, description FROM books;
**Update (UPDATE)**
  - Used to modify existing records.
**UPDATE books**
  - SET description = "An In-Depth Guide to Android's Security Architecture."
  - WHERE id = 1;
  - Always combine with WHERE to avoid updating all rows.
**Delete (DELETE)**
  - Used to remove records.
  - DELETE FROM books WHERE id = 1;
  - Without WHERE, all rows will be deleted (dangerous!).

### Notes
- CRUD = foundation of database operations.
- INSERT → add new entries.
- SELECT → fetch data (all or filtered).
- UPDATE → change existing data.
- DELETE → remove data.
- WHERE clause is critical in UPDATE and DELETE to target specific rows.
- These statements map directly to real-world data operations (e.g., adding a new user, checking posts, editing profile info, or removing an account).


## SQL Clauses

### Concepts Learned
- Clauses refine SQL queries by adding conditions, grouping, or sorting results.

### Explanation
**DISTINCT**
  - Removes duplicate values from the query result.
  - SELECT DISTINCT name FROM books;
  - Ensures only unique records are returned.
**GROUP BY**
  - Groups rows that have the same values in specified columns.
  - Often used with aggregate functions (COUNT, SUM, AVG).
  - SELECT name, COUNT(*) 
    FROM books
    GROUP BY name;
  - Example: shows “Ethical Hacking” appears twice.
**ORDER BY**
  - Sorts query results.
  - By default → ascending (ASC), can specify descending (DESC).
  - SELECT * FROM books ORDER BY published_date ASC;  
  - SELECT * FROM books ORDER BY published_date DESC;
- Helps organize results based on numerical or date values.
**HAVING**
  - Filters results after grouping/aggregation (unlike WHERE, which works before).
  - SELECT name, COUNT(*)
    FROM books
    GROUP BY name
    HAVING name LIKE '%Hack%';
- Example: filters only groups containing “Hack” in the name.

### Notes
- Clauses refine queries for cleaner, more meaningful results.
- DISTINCT → removes duplicate entries.
- GROUP BY → groups rows and pairs well with aggregate functions.
- ORDER BY → sorts query results (ASC = oldest first, DESC = newest first).
- HAVING → filters aggregated data, while WHERE filters raw data before aggregation.
- Best practice: always pair GROUP BY with aggregate functions and use HAVING for conditions after aggregation.


## Operators

### Concepts Learned
- Operators allow filtering and manipulating data with conditions in SQL.
**Two major categories:**
  - Logical operators (work with boolean logic).
  - Comparison operators (compare values for equality/inequality).

### Explanation
**Logical Operators**
  - LIKE – pattern matching using wildcards (% for any sequence, _ for single character).
    - Example: WHERE description LIKE "%guide%" → finds rows containing guide.
  - AND – combines multiple conditions; all must be TRUE.
    - Example: WHERE category = "Offensive Security" AND name = "Bug Bounty Bootcamp".
  - OR – at least one condition must be TRUE.
    - Example: WHERE name LIKE "%Android%" OR name LIKE "%iOS%".
  - NOT – negates a condition.
    - Example: WHERE NOT description LIKE "%guide%".
  - BETWEEN – checks if a value falls within a range.
    - Example: WHERE id BETWEEN 2 AND 4.
**Comparison Operators**
  - = (Equal To) – matches exact values.
    - Example: WHERE name = "Designing Secure Software".
  - != (Not Equal To) – excludes certain values.
    - Example: WHERE category != "Offensive Security".
  - < (Less Than) – matches values lower than given.
    - Example: WHERE published_date < "2020-01-01".
  - > (Greater Than) – matches values greater than given.
    - Example: WHERE published_date > "2020-01-01".
  - <= (Less Than or Equal To) – matches values less than or equal.
    - Example: WHERE published_date <= "2021-11-15".
  - >= (Greater Than or Equal To) – matches values greater than or equal.
    - Example: WHERE published_date >= "2021-11-02".

### Notes
- Logical operators define filtering logic (pattern search, ranges, boolean conditions).
- Comparison operators define value-based filtering.
- Combining operators with clauses like WHERE, ORDER BY, and HAVING creates powerful queries.
- % is the most used wildcard with LIKE (matches zero or more characters).
- BETWEEN is inclusive → includes both boundary values.


## Functions

### Concepts Learned
- SQL functions simplify operations on data.
**Two major categories:**
  - String functions – operate on text.
  - Aggregate functions – operate across multiple rows.

### Explanation
**String Functions**
  - CONCAT() – joins two or more strings.
    - Example: SELECT CONCAT(name, " is a type of ", category, " book.") AS book_info FROM books;
    - Output: "Android Security Internals is a type of Defensive Security book."
  - GROUP_CONCAT() – combines multiple row values into a single string, grouped by a column.
    - Example: SELECT category, GROUP_CONCAT(name SEPARATOR ", ") FROM books GROUP BY category;
    - Groups book names under their categories.
  - SUBSTRING() – extracts part of a string based on position and length.
    - Example: SELECT SUBSTRING(published_date, 1, 4) AS published_year FROM books;
    - Extracts the year from date values.
  - LENGTH() – returns the number of characters in a string (spaces included).
    - Example: SELECT LENGTH(name) FROM books;
    - Finds length of book titles.
**Aggregate Functions**
  - COUNT() – counts number of rows (or values in a column).
    - Example: SELECT COUNT(*) AS total_books FROM books; → 5
  - SUM() – adds up numeric values in a column (ignores NULLs).
    - Example: SELECT SUM(price) AS total_price FROM books;
  - MAX() – returns maximum value from a column.
    - Example: SELECT MAX(published_date) FROM books; → latest book date.
  - MIN() – returns minimum value from a column.
    - Example: SELECT MIN(published_date) FROM books; → earliest book date.

### Notes
- String functions help with text manipulation and formatting (concatenating, extracting, measuring length).
- Aggregate functions are essential for reporting, summarizing, and analytics.
- GROUP_CONCAT + GROUP BY are powerful for turning multiple rows into readable combined results.
- Aggregate functions often used with GROUP BY and HAVING clauses.


## Key Takeaways
- SQL (Structured Query Language) is the standard language for managing and manipulating relational databases.
- CRUD operations (Create, Read, Update, Delete) are the foundation of working with data.
- Clauses like WHERE, GROUP BY, ORDER BY, HAVING, and DISTINCT refine and organize query results.
- Operators (logical & comparison) allow filtering and condition-building for precise queries.
- Functions (string and aggregate) provide advanced ways to manipulate and summarize data.
- Combining clauses, operators, and functions allows building powerful queries for reporting, analytics, and data transformation.
- Best practice: Always use WHERE or HAVING with care to avoid unintended changes/deletions.
- Understanding these fundamentals is essential before moving to advanced SQL topics like joins, subqueries, indexing, and security.
