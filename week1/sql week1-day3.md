**SQL Training Notes Day-3(12-02-2024)**

**SQL Revision Notes - Foreign Keys, Normalization, Stored Procedures, ACID, and Indexes**

This document provides concise notes for revision on Foreign Keys, Normalization, Stored Procedures, ACID properties, and Indexes in SQL.

**I. Foreign Keys**

- **Definition:** A constraint that enforces referential integrity between two tables. A foreign key in the child table references a primary key (or unique key) in the parent table.
- **Purpose:** Prevents orphaned records, maintains data consistency.
- **Characteristics:**
  - References a primary/unique key in another table.
  - Enforces referential integrity.
  - Parent table's referenced column must be unique.
  - Actions on UPDATE/DELETE can be defined (CASCADE, SET NULL, RESTRICT, NO ACTION).
- **Example:**

CREATE TABLE Departments (DeptID INT PRIMARY KEY, DeptName VARCHAR(50));

CREATE TABLE Employees (EmpID INT PRIMARY KEY, Name VARCHAR(50), DeptID INT, FOREIGN KEY (DeptID) REFERENCES Departments(DeptID));

- **ON DELETE/UPDATE Actions:**
  - CASCADE: Child records are deleted/updated when the parent record is deleted/updated.
  - SET NULL: Foreign key in child table is set to NULL.
  - RESTRICT/NO ACTION: Prevents deletion/update if references exist.
- **ER Diagrams:** Foreign keys are represented by a line connecting the two entities, often with a "many" symbol on the child table side (e.g., one department can have many employees).

**II. Database Normalization**

- **Purpose:** Reduce data redundancy and improve data integrity. Breaks down large tables into smaller, related tables.
- **Benefits:**
  - Reduced redundancy.
  - Improved data integrity.
  - Eliminated anomalies (insert, update, delete).
  - Enhanced query performance.
- **Normal Forms:**
  - **1NF:** Atomic values, no repeating groups.
  - **2NF:** 1NF + No partial dependencies (non-key attributes depend on the _full_ primary key).
  - **3NF:** 2NF + No transitive dependencies (non-key attributes don't depend on other non-key attributes).
  - **BCNF:** Every determinant is a candidate key.
- **Example (Simplified):** A table with StudentID, CourseID, StudentName, and CourseName would be split into separate Student, Course, and Enrollment tables to eliminate redundancy.

**III. Stored Procedures**

- **Definition:** Precompiled set of SQL statements stored in the database.
- **Benefits:**
  - Reusability.
  - Performance boost.
  - Enhanced security (prevents SQL injection).
  - Encapsulation of logic.
  - Reduced network traffic.
- **Syntax (Example):**

DELIMITER //

CREATE PROCEDURE GetEmployeesByDept(IN dept_name VARCHAR(50))

BEGIN

SELECT \* FROM Employees WHERE Department = dept_name;

END //

DELIMITER ;

CALL GetEmployeesByDept('IT');

- **Parameters:** IN (input), OUT (output), INOUT.

**IV. ACID Properties**

- **Guarantees of reliable database transactions:**
  - **Atomicity:** All or nothing. A transaction is either fully completed or rolled back.
  - **Consistency:** Maintains database integrity. Transactions move the database from one valid state to another.
  - **Isolation:** Transactions don't interfere with each other.
  - **Durability:** Once a transaction is committed, it's permanent, even in the event of system failure.

**V. Indexes**

- **Purpose:** Improve the speed of data retrieval operations. Like an index in a book.
- **Types:**
  - **Clustered:** Physically sorts the table rows. One per table.
  - **Non-clustered:** Logical ordering, separate structure. Multiple per table.
  - **Unique:** Ensures unique values.
  - **Composite:** Index on multiple columns.
- **Creation (Example):**

CREATE INDEX idx_name ON Employees (Name);

CREATE UNIQUE INDEX idx_email ON Employees (Email);

- **Considerations:**
  - Speed up reads, slow down writes.
  - Use for frequently queried columns, small subsets of data.
  - Avoid for small tables, frequently updated columns, low uniqueness columns.

**VI. Key Terms Summary**

| **Term** | **Description** |
| --- | --- |
| Foreign Key | Links tables, enforces referential integrity |
| Normalization | Reduces data redundancy, improves integrity |
| Stored Procedure | Precompiled SQL code, reusable, improves performance |
| ACID | Guarantees of reliable database transactions |
| Index | Speeds up data retrieval |

This revised structure is optimized for pasting into a Word document and serves as a concise revision guide. Remember to practice writing SQL queries and working with databases to reinforce your understanding.

Question 1: <https://leetcode.com/problems/project-employees-i/?envType=study-plan-v2&envId=top-sql-50>


Solved some other problems in leetcode.
