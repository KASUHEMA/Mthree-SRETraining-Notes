**SRE Day-4 Revision Notes: MySQL and Git with Commands**

**MySQL:**

- **Creating and Populating Tables:**
  - CREATE TABLE table_name (columns);
  - INSERT INTO table_name VALUES (values);
  - SELECT \* INTO new_table FROM existing_table;

Create and populate source table

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

\-- Generate INSERT statements from SELECT

SELECT CONCAT(

'INSERT INTO employees (emp_id, name, salary, department) VALUES (',

emp_id, ', ',

QUOTE(name), ', ',

salary, ', ',

QUOTE(department), ');'

) AS insert_statement

FROM source_employees;

This is to show what happens if we delete row from child table

INSERT INTO courses VALUES (1, 'Mathematics', 3);

# INSERT INTO students VALUES (1, 'John', 'Doe', '[john@email.com](mailto:john@email.com)');

INSERT INTO enrollments VALUES (1, 1, 1, '2025-02-12');

delete from courses where course_id =1;

select \* from enrollments;

select \* from courses

create table enrollments(

enrollment_id int primary key,

student_id int,

course_id int,

enrollment_date date,

foreign key(student_id) references students(student_id),

foreign key(course_id) references courses(course_id)

on delete cascade

);

- **ON DELETE CASCADE / ON UPDATE CASCADE:**
  - Used to maintain referential integrity between parent and child tables.
  - FOREIGN KEY (column) REFERENCES parent_table(column) ON DELETE CASCADE ON UPDATE CASCADE;
  - **ON DELETE CASCADE:** Automatically deletes rows in child table when corresponding row in parent table is deleted.
  - **ON UPDATE CASCADE:** Automatically updates values in child table when corresponding row in parent table is updated.
- **Triggers:**

Special stored procedures that run automatically when certain events occur.

**Syntax:**

CREATE TRIGGER trigger_name

BEFORE/AFTER INSERT/UPDATE/DELETE ON table_name

FOR EACH ROW

BEGIN

\-- SQL statements

END;

**Example:**

**CREATE TRIGGER log_delete**

**AFTER DELETE ON employees**

**FOR EACH ROW**

**BEGIN**

**INSERT INTO employee_log VALUES (OLD.id, NOW(), 'Deleted');**

**END;**

**COALESCE**

SELECT

e.emp_id,

[e.name](http://e.name/),

COALESCE(CAST(d.department_id AS CHAR), 'No Department Assigned') AS department_id,

COALESCE(d.department_name, 'No Department Assigned') AS department_name,

COALESCE(d.location, 'No Location Assigned') AS location

FROM employees e

LEFT JOIN departments d

ON e.emp_id = d.department_id;

used coalesce to add message in the department when there is null value

and use cast to allow string in the integer coulmn

**Terminal Basics:**

- **Commands:**
  - mkdir folder_name – Create folder
  - ls -la – List all files (including hidden)
  - man command_name – View manual for commands
  - touch file_name – Create file
  - rm file_name – Remove file
  - rm -rf folder_name – Remove folder forcefully
  - cd path – Change directory
  - pwd – Show current directory

**Git Basics:**

- **Initialize Repository:**
  - git init – Initialize Git in current folder
- **Clone Repository:**
  - git clone repository_link – Clone remote repo
- **Track Changes:**
  - git status – Show status
  - git add . – Stage all changes
  - git commit -m "message" – Commit with message
- **Push Changes:**
  - git push origin main – Push to main branch
  - git push -u origin main – Set upstream branch
- **Pull Changes:**
  - git pull origin main – Pull from remote
- **Branching:**
  - git branch – List branches
  - git checkout -b branch_name – Create and switch to new branch
  - git merge branch_name – Merge branch to main
- **Reset Changes:**
  - git reset file_name – Unstage file
  - git reset HEAD~1 – Undo last commit
  - git reset --hard – Discard all changes

**Create the file (if it doesn't exist) and open it in Vim:**

vi first.txt

**Enter Insert Mode (to start writing):**

Press the i key.

You should see -- INSERT -- at the bottom of the Vim window, indicating that you're now in insert mode. You can now start typing your text.

**Write your content:**

Type the text you want to include in the file.

**Exit Insert Mode (to save and exit):**

- Press the Esc key. This will take you out of insert mode and back to normal mode (command mode).

**Save and Exit:**

- Type :wq and press Enter. This command does the following:
- w: Writes (saves) the file.
- q: Quits Vim.

**Summary:**

- Master MySQL table creation, constraints, triggers, and cascades.
- Use terminal commands for file management.
- Manage version control with Git commands for cloning, branching, committing, pushing, pulling, and resetting.

In the afternoon in beakout rooms we discussed about git commands as some student in our break out room is facing issues and then we solved some coding questions on leetcode and screenshots are
![image](https://github.com/user-attachments/assets/97b9aa3f-c3f2-4271-af3b-53cc03740e91)
![image](https://github.com/user-attachments/assets/6af708eb-e8f3-4b5e-a901-e0f266a732f3)
![image](https://github.com/user-attachments/assets/ee2adfed-0115-429f-8a2e-ac8d4bd67ce6)



