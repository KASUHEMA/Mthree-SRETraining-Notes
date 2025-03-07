# SRE Day-4 Revision Notes: MySQL and Git with Commands

## MySQL

### Creating and Populating Tables

```sql
-- Create and populate source table
CREATE TABLE source_employees (
    emp_id INT PRIMARY KEY,
    name VARCHAR(50),
    salary DECIMAL(10,2),
    department VARCHAR(50)
);

INSERT INTO source_employees VALUES
    (1, 'John Smith', 50000, 'IT'),
    (2, 'Sarah Johnson', 60000, 'HR'),
    (3, 'Michael Brown', 55000, 'IT');
```

### Generate INSERT Statements from SELECT

```sql
SELECT CONCAT(
    'INSERT INTO employees (emp_id, name, salary, department) VALUES (',
    emp_id, ', ',
    QUOTE(name), ', ',
    salary, ', ',
    QUOTE(department), ');'
) AS insert_statement
FROM source_employees;
```

### Foreign Keys and ON DELETE CASCADE

```sql
CREATE TABLE enrollments (
    enrollment_id INT PRIMARY KEY,
    student_id INT,
    course_id INT,
    enrollment_date DATE,
    FOREIGN KEY(student_id) REFERENCES students(student_id),
    FOREIGN KEY(course_id) REFERENCES courses(course_id)
    ON DELETE CASCADE
);

INSERT INTO courses VALUES (1, 'Mathematics', 3);
INSERT INTO enrollments VALUES (1, 1, 1, '2025-02-12');

DELETE FROM courses WHERE course_id = 1;
SELECT * FROM enrollments;
SELECT * FROM courses;
```

### Triggers

```sql
CREATE TRIGGER log_delete
AFTER DELETE ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_log VALUES (OLD.id, NOW(), 'Deleted');
END;
```

### COALESCE Example

```sql
SELECT
    e.emp_id,
    e.name,
    COALESCE(CAST(d.department_id AS CHAR), 'No Department Assigned') AS department_id,
    COALESCE(d.department_name, 'No Department Assigned') AS department_name,
    COALESCE(d.location, 'No Location Assigned') AS location
FROM employees e
LEFT JOIN departments d
ON e.emp_id = d.department_id;
```

## Terminal Basics

### Common Commands

```
mkdir folder_name      # Create folder
ls -la                # List all files (including hidden)
man command_name      # View manual for commands
touch file_name       # Create file
rm file_name          # Remove file
rm -rf folder_name    # Remove folder forcefully
cd path               # Change directory
pwd                   # Show current directory
```

## Git Basics

### Initializing and Cloning

```
git init              # Initialize Git in current folder
git clone repository_link  # Clone remote repo
```

### Tracking Changes

```
git status            # Show status
git add .             # Stage all changes
git commit -m "message"  # Commit with message
```

### Pushing Changes

```
git push origin main       # Push to main branch
git push -u origin main    # Set upstream branch
```

### Pulling Changes

```
git pull origin main  # Pull from remote
```

### Branching

```
git branch               # List branches
git checkout -b new_branch  # Create and switch to new branch
git merge branch_name    # Merge branch to main
```

### Resetting Changes

```
git reset file_name      # Unstage file
git reset HEAD~1         # Undo last commit
git reset --hard         # Discard all changes
```

## Working with Vim

### Creating a File and Opening Vim

```
vi first.txt
```

### Enter Insert Mode

```
Press `i`
```

### Save and Exit

```
Press `Esc`, then type `:wq` and press Enter
```

## Summary

- Master MySQL table creation, constraints, triggers, and cascades.
- Use terminal commands for file management.
- Manage version control with Git commands for cloning, branching, committing, pushing, pulling, and resetting.

## Breakout Room Discussion

- Discussed Git commands and resolved some issues.
- Solved coding questions on LeetCode.

### Screenshots

In the afternoon in beakout rooms we discussed about git commands as some student in our break out room is facing issues and then we solved some coding questions on leetcode and screenshots are
![image](https://github.com/user-attachments/assets/97b9aa3f-c3f2-4271-af3b-53cc03740e91)
![image](https://github.com/user-attachments/assets/6af708eb-e8f3-4b5e-a901-e0f266a732f3)
![image](https://github.com/user-attachments/assets/ee2adfed-0115-429f-8a2e-ac8d4bd67ce6)



