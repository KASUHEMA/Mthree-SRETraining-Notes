**SQL Learning Report – Day 2( 11-02-2025)**

***1\. Bitwise Operations***

Bitwise operations manipulate data at the binary level. They are useful for managing permissions, flags, and optimizing certain calculations.

- **Key Operators:**
  - | (OR): Sets a bit if it's set in either operand.
  - & (AND): Sets a bit only if it's set in both operands.
  - ^ (XOR): Sets a bit if it's set in either operand, but not both.
  - ~ (NOT): Inverts all bits.
- **Example (Permission Management):**

| **Permission** | **Binary** | **Value** |
| --- | --- | --- |
| Read | 100 | 4   |
| Write | 010 | 2   |
| Execute | 001 | 1   |

- **Queries:**
  - Add Write Permission: UPDATE permissions SET permission_flags = permission_flags | 2 WHERE (permission_flags & 2) = 0;
  - Toggle Execute Permission: UPDATE permissions SET permission_flags = permission_flags ^ 1;
  - Check Read Permission: SELECT user_id, username, CASE WHEN (permission_flags & 4) > 0 THEN 'Has Read Permission' ELSE 'No Read Permission' END AS ReadPermissionStatus FROM permissions;

**2\. Bit Shifting Operations**

Bit shifting efficiently multiplies or divides by powers of 2.

- **Operators:**
  - << (Left Shift): Multiplies by 2 for each shift.
  - \>> (Right Shift): Divides by 2 for each shift.
- **Example:**

| **Value** | **Binary** | **<< 1** | **Binary** | **<< 2** | **Binary** | **\>> 1** | **Binary** | **\>> 2** | **Binary** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8   | 1000 | 16  | 10000 | 32  | 100000 | 4   | 0100 | 2   | 0010 |
| 12  | 1100 | 24  | 11000 | 48  | 110000 | 6   | 0110 | 3   | 0011 |
| 16  | 10000 | 32  | 100000 | 64  | 1000000 | 8   | 01000 | 4   | 00100 |

**3\. SQL Clauses (NOT, BETWEEN, EXISTS)**

These clauses filter data based on specific conditions.

- NOT: Inverts a condition. SELECT \* FROM Products WHERE InStock != 0; (Finds products in stock).
- BETWEEN: Filters values within a range. SELECT \* FROM Orders WHERE TotalAmount BETWEEN 1000 AND 2000;
- EXISTS: Checks for the existence of records in a subquery. SELECT Name FROM Customers C WHERE EXISTS (SELECT 1 FROM Orders O WHERE O.CustomerID = C.CustomerID); (Finds customers with at least one order).

**4\. SQL Joins**

Joins combine data from multiple tables based on related columns.

- **INNER JOIN:** Returns only matching rows from both tables.
- **LEFT JOIN:** Returns all rows from the left table and matching rows from the right table (NULLs for non-matches).
- **RIGHT JOIN:** Returns all rows from the right table and matching rows from the left table (NULLs for non-matches).
- **Example:**

SELECT E.Name, D.DeptName

FROM Employees E

INNER JOIN Departments D ON E.DeptID = D.DeptID;

| **Join Type** | **Includes Non-Matching Records?** | **Which Table Shows All Records?** |
| --- | --- | --- |
| INNER JOIN | No  | Only matching records |
| LEFT JOIN | Yes (from left table) | Left |
| RIGHT JOIN | Yes (from right table) | Right |

**5\. SQL Ranking Functions**

Ranking functions assign ranks to rows based on a specified order.

- RANK(): Assigns the same rank to duplicates, skips ranks.
- DENSE_RANK(): Assigns the same rank to duplicates, does not skip ranks.
- PARTITION BY: Calculates ranks within groups.
- **Example:**

SELECT EmployeeID, Name, Salary,

RANK() OVER (ORDER BY Salary DESC) AS RankValue,

DENSE_RANK() OVER (ORDER BY Salary DESC) AS DenseRankValue

FROM Employees;

**6\. LAG() Function**

The LAG() function accesses data from a previous row within a result set.

- **Example:**

SELECT EmployeeID, Name, Salary,

LAG(Salary, 1, 0) OVER (ORDER BY Salary DESC) AS PreviousSalary

FROM Employees;

**7\. UNION and UNION ALL**

These operators combine the results of multiple SELECT queries.

- UNION: Removes duplicate rows.
- UNION ALL: Keeps all rows, including duplicates.
- **Example:**

SELECT \* FROM EmployeesIndia

UNION

SELECT \* FROM EmployeesUSA;

| **Feature** | **UNION** | **UNION ALL** |
| --- | --- | --- |
| Removes Duplicates? | Yes | No  |
| Performance | Slower | Faster |
| Use Case | Unique values | All records (including duplicates) |

Question 1: 
<https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/?envType=study-plan-v2&envId=top-sql-50>
![image](https://github.com/user-attachments/assets/686a8fb3-3018-40d9-b562-6fceb5148fa4)

Question 2:
<https://leetcode.com/problems/product-sales-analysis-i/?envType=study-plan-v2&envId=top-sql-50>
![image](https://github.com/user-attachments/assets/06cbcf6b-c83a-45bd-bc7e-4ea12ed49515)

Question 3:
<https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/description/?envType=study-plan-v2&envId=top-sql-50>
![image](https://github.com/user-attachments/assets/52a14ea9-a288-40cc-af37-70b1468f563b)

Question 4:
<https://leetcode.com/problems/employee-bonus/?envType=study-plan-v2&envId=top-sql-50>
![image](https://github.com/user-attachments/assets/c4eb30be-aaa6-40de-87b6-19a352925566)

Question 5:
<https://leetcode.com/problems/managers-with-at-least-5-direct-reports/?envType=study-plan-v2&envId=top-sql-50>
![image](https://github.com/user-attachments/assets/507cf0d3-b917-4745-8107-3d3168bff7ec)

Question 6:
<https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/submissions/1541924953/?envType=study-plan-v2&envId=top-sql-50>
![image](https://github.com/user-attachments/assets/0df7053e-bf55-455a-8b12-b084b4748a5e)
