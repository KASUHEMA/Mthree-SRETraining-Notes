# SQL Learning Documentation - 10-02-2025 (DAY-1)

## I. Introduction
- **Database**: A structured collection of data.
- **DBMS (Database Management System)**: Software to interact with databases (e.g., MySQL, PostgreSQL, MongoDB).
- **RDBMS (Relational DBMS)**: Uses tables (MySQL, PostgreSQL).
- **NoSQL DBMS**: Uses other structures like key-value pairs, documents (MongoDB).

## II. Core SQL Concepts & Commands
- **Rows**: Represent individual data items (e.g., a single shirt).
- **Columns**: Represent attributes of the data (e.g., color, size).
- **Tables**: Collections of rows and columns (e.g., a table for "Shirts").
- **SQL Query**: A request to the database (e.g., "Show me all pink shirts").

### A. DDL (Data Definition Language): Modifies database structure (CREATE, ALTER, DROP)
```sql
CREATE TABLE employees (id INT, name VARCHAR(50), salary INT);
ALTER TABLE employees ADD COLUMN department VARCHAR(50);
DROP TABLE employees;
```

### B. DML (Data Manipulation Language): Modifies data within tables (UPDATE, INSERT, DELETE, TRUNCATE)
```sql
INSERT INTO employees (id, name, salary) VALUES (1, 'John', 50000);
UPDATE employees SET salary = 55000 WHERE id = 1;
DELETE FROM employees WHERE id = 1;
TRUNCATE TABLE employees;
```

## III. Table Manipulation & Queries
### Cloning Tables
- **Deep Copy**: Copies structure and data.
```sql
CREATE TABLE new_table AS SELECT * FROM old_table;
```
- **Shallow Copy**: Copies only structure.
```sql
CREATE TABLE new_table LIKE old_table;
```

### Other Queries
```sql
DESC employees; -- Describes table structure
CREATE TEMPORARY TABLE temp_table AS SELECT * FROM employees;
CREATE VIEW high_salary AS SELECT * FROM employees WHERE salary > 60000;
```

## IV. Data Types & Constraints
- **CHAR**: Fixed-length string (e.g., PIN codes).
- **VARCHAR**: Variable-length string (e.g., names).
- **ORDER BY**: Sorts results.
```sql
SELECT * FROM employees ORDER BY salary DESC;
```
- **HAVING**: Filters grouped results.
```sql
SELECT department, COUNT(*) FROM employees GROUP BY department HAVING COUNT(*) > 5;
```
- **WHERE**: Filters rows.
```sql
SELECT * FROM employees WHERE salary > 50000;
```
- **LIMIT**: Restricts the number of results.
```sql
SELECT * FROM employees LIMIT 5;
```
- **DISTINCT**: Finds unique values.
```sql
SELECT DISTINCT department FROM employees;
```

### Constraints
- **Primary Key**: Unique identifier for each row (NOT NULL, automatically indexed). One per table.
- **UNIQUE**: Ensures unique values in a column (allows NULLs). Multiple allowed.
- **NOT NULL**: Ensures a column cannot have NULL values.

## V. Key Differences & Concepts
- **DELETE vs. TRUNCATE**: DELETE is slower, allows rollback, removes specific rows. TRUNCATE is faster, no rollback, removes all rows.
- **PRIMARY KEY vs. UNIQUE**: PRIMARY KEY is NOT NULL, one per table, automatically indexed. UNIQUE allows NULLs, multiple allowed, indexed but not always automatic.

## VI. MySQL Workbench
- Download and install from the official MySQL website.
- Connect to your database to execute SQL queries.

## LeetCode SQL 50 Problems
- [Recyclable and Low-Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/description/?envType=study-plan-v2&envId=top-sql-50)
  ![SQL Query Execution](https://github.com/user-attachments/assets/636f3bd2-2710-4321-ad50-6a7dd13f4986)

- [Find Customer Referee](https://leetcode.com/problems/find-customer-referee/?envType=study-plan-v2&envId=top-sql-50)
  ![SQL Query Execution](https://github.com/user-attachments/assets/c9903584-55df-4f3e-b25e-8e07896bdfcc)

- [Big Countries](https://leetcode.com/problems/big-countries/description/?envType=study-plan-v2&envId=top-sql-50)
  ![image](https://github.com/user-attachments/assets/c048b03f-c2b6-485d-89d5-eb4fb6c08cde)

- [Article Views I](https://leetcode.com/problems/article-views-i/description/?envType=study-plan-v2&envId=top-sql-50)
- ![image](https://github.com/user-attachments/assets/84963ec4-1e9c-4edf-9670-0cb3d14ff7db)

- [Invalid Tweets](https://leetcode.com/problems/invalid-tweets/description/?envType=study-plan-v2&envId=top-sql-50)
  ![image](https://github.com/user-attachments/assets/ee308411-f972-4452-a85a-d4c0c510428f)

- [Average Selling Price](https://leetcode.com/problems/average-selling-price/?envType=study-plan-v2&envId=top-sql-50)
  ![image](https://github.com/user-attachments/assets/757631b1-fac3-42fa-a107-1c1d548a046c)

  ![Not boring-movies](https://github.com/user-attachments/assets/739f1463-c9d4-4d83-adf0-fefa86243939)


### Solved additional questions on:
- Aggregate functions like COUNT, SUM, and AVG.
- SQL techniques such as SELECT, ORDER BY, DISTINCT, DESC, etc.

## Conclusion
In this report, I explored the concepts of cloning tables in MySQL, specifically the differences between shallow and deep copies, where a shallow copy only duplicates table references while a deep copy duplicates both the structure and data. I also gained practical experience using MySQL Workbench to execute SQL commands and visualize data. Additionally, I solved LeetCode problems related to table cloning and aggregate functions like COUNT, SUM, and AVG, along with SELECT, ORDER BY, DISTINCT, DESC, etc., which enhanced my understanding of SQL techniques for efficient data manipulation. Overall, this hands-on learning reinforced both my theoretical and practical knowledge of MySQL, preparing me for more complex database management tasks.


