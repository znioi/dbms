# 💾 DBMS Experiment 2 – DDL and DML Queries (MySQL Workbench)


---

## 🧠 Objective

Implement basic SQL commands for DDL (create, alter, drop, etc.) and DML (insert, update, delete, etc.) operations on a relational database.

---

## 📚 Theory Overview

### 🔹 DDL Commands

- CREATE: Create new tables
- ALTER: Modify existing table structure (add, drop, modify columns)
- RENAME: Rename a table
- TRUNCATE: Remove all data from a table without deleting the structure
- DROP: Permanently remove the table

Example:
```sql
CREATE TABLE emp (
    empno INT PRIMARY KEY,
    ename VARCHAR(10)
);
ALTER TABLE emp ADD salary DECIMAL(7,2);
ALTER TABLE emp DROP COLUMN salary;
ALTER TABLE emp MODIFY ename VARCHAR(15);
RENAME TABLE emp TO emp1;
TRUNCATE TABLE emp1;
DROP TABLE emp1;
```

### 🔹 DML Commands

- INSERT: Add new rows
- DELETE: Remove existing rows
- UPDATE: Modify values in existing rows

Example:
```sql
INSERT INTO emp1 (empno, ename) VALUES (101, 'Alice');
DELETE FROM emp1 WHERE empno = 101;
UPDATE emp1 SET salary = salary + 500 WHERE empno = 102;
```

---

## ⚙️ SQL Tasks and Commands

### 🏗️ DDL Section

1. Create table VIPS:
```sql
CREATE TABLE VIPS (
    id INT PRIMARY KEY,
    name VARCHAR(30) NOT NULL,
    age INT CHECK(age > 18),
    city VARCHAR(20),
    salary DECIMAL(10, 2),
    comm DECIMAL(6,2) DEFAULT 0,
    dept_id INT
);
```

2. Create table VIPSTC and add constraints:
```sql
CREATE TABLE VIPSTC (
    id INT,
    name VARCHAR(30),
    age INT,
    city VARCHAR(20),
    salary DECIMAL(10, 2),
    comm DECIMAL(6,2),
    dept_id INT
);

ALTER TABLE VIPSTC 
ADD CONSTRAINT pk_id PRIMARY KEY(id),
ADD CONSTRAINT uq_name UNIQUE(name),
ADD CONSTRAINT nn_city CHECK(city IS NOT NULL),
ADD CONSTRAINT chk_age CHECK(age >= 18),
ADD CONSTRAINT def_comm DEFAULT 0 FOR comm;
```

3. Modify VIPS:
```sql
ALTER TABLE VIPS ADD (
    Commission DECIMAL(6,2),
    Phone VARCHAR(10)
);

ALTER TABLE VIPS DROP COLUMN Phone;

ALTER TABLE VIPS MODIFY salary DECIMAL(12,2);
```

4. Rename column and table:
```sql
ALTER TABLE VIPS RENAME COLUMN name TO emp_name;
RENAME TABLE VIPS TO VSET;
```

5. Create VIPS1 and VIPSTC1:
```sql
CREATE TABLE VIPS1 (
    ID INT,
    NAME VARCHAR(30),
    STATE VARCHAR(20),
    SAL DECIMAL(10,2),
    Dno INT
);

CREATE TABLE VIPSTC1 (
    ID INT,
    NAME VARCHAR(30),
    STATE VARCHAR(20),
    SAL DECIMAL(10,2),
    Dno INT
);
```

6. Drop & Truncate:
```sql
DROP TABLE VIPS1;
TRUNCATE TABLE VIPSTC1;
```

---

### ✍️ DML Section

1. Insert values:
```sql
INSERT INTO VSET VALUES (1, 'Arjun', 25, 'Pune', 6000, 200, 10);
-- Repeat for 6 more entries...
```

2. Show full table:
```sql
SELECT * FROM VSET;
```

3. Select 3 columns:
```sql
SELECT emp_name, age, salary FROM VSET;
SELECT emp_name, age, salary FROM VSET WHERE city = 'Pune';
```

4. Update salary by 3000:
```sql
UPDATE VSET SET salary = salary + 3000 WHERE id = 2;
```

5. Update commission:
```sql
UPDATE VSET SET comm = comm + 100;
```

6. Update salary conditionally:
```sql
UPDATE VSET SET salary = salary + 500 WHERE salary BETWEEN 5000 AND 6000;
```

7. Update salary by 10%:
```sql
UPDATE VSET SET salary = salary * 1.10 WHERE id = 7 OR salary < 3000;
```

8. Delete employee based on salary and comm:
```sql
DELETE FROM VSET WHERE salary BETWEEN 5000 AND 5500 AND comm < 5;
```

9. Delete employee by department:
```sql
DELETE FROM VSET WHERE dept_id IS NOT NULL;
```

10. Delete employee with no commission:
```sql
DELETE FROM VSET WHERE comm IS NULL OR comm = 0;
```

---

## ✅ Learning Outcomes

- Ability to define, modify, and delete schema structures using DDL commands.
- Perform CRUD operations using DML commands.
- Understand constraints and data integrity in SQL.
- Use MySQL Workbench to write, execute and debug SQL queries effectively.

---
---
---

---
---

# 🎓 DBMS Experiment 2 – Viva Questions & Answers

---

## 🧠 Basic Conceptual Questions

### 1. What is the difference between DDL and DML?

- DDL (Data Definition Language): Commands that define or modify the structure of database objects like tables.
  - Examples: CREATE, ALTER, DROP, RENAME, TRUNCATE
- DML (Data Manipulation Language): Commands used to manipulate data within the database.
  - Examples: INSERT, UPDATE, DELETE

---

### 2. What is the purpose of the CREATE TABLE command?

- It is used to create a new table with specified columns, data types, and constraints.

Example:
```sql
CREATE TABLE student (
  id INT PRIMARY KEY,
  name VARCHAR(50)
);
```

---

### 3. How do you modify a column in a table?

- Use the ALTER TABLE … MODIFY statement.

Example:
```sql
ALTER TABLE student MODIFY name VARCHAR(100);
```

---

### 4. What is the difference between TRUNCATE and DELETE?

- TRUNCATE: Deletes all rows from a table, faster and does not generate individual row delete logs. Cannot be rolled back.
- DELETE: Deletes rows based on a condition or all rows. Can be rolled back if inside a transaction.

---

### 5. What is the difference between DROP and TRUNCATE?

- DROP: Completely removes the table structure and data.
- TRUNCATE: Removes only the data, structure remains.

---

## ⚙️ SQL Syntax-Based Questions

### 6. How do you add a new column to an existing table?

```sql
ALTER TABLE tablename ADD column_name DATATYPE(SIZE);
```

Example:
```sql
ALTER TABLE emp ADD phone VARCHAR(10);
```

---

### 7. Write SQL command to rename a table.

```sql
RENAME TABLE old_name TO new_name;
```

Example:
```sql
RENAME TABLE emp TO emp1;
```

---

### 8. Write SQL command to delete employees with no commission.

```sql
DELETE FROM emp WHERE comm IS NULL OR comm = 0;
```

---

### 9. How do you update the salary of employees whose salary is between 5000 and 6000?

```sql
UPDATE emp SET salary = salary + 500 WHERE salary BETWEEN 5000 AND 6000;
```

---

### 10. What does the CHECK constraint do?

- It restricts the value that can be inserted into a column based on a condition.

Example:
```sql
age INT CHECK(age > 18)
```

---

## 🔐 Constraints and Integrity

### 11. What is a Primary Key?

- A unique identifier for each record in a table. Cannot have NULL or duplicate values.

---

### 12. What is a Unique Key?

- Ensures all values in a column are unique. Can have NULL (once).

---

### 13. What is the Default constraint?

- Assigns a default value to a column when no value is specified during insert.

Example:
```sql
comm DECIMAL(5,2) DEFAULT 0
```

---

### 14. How do you delete a column from a table?

```sql
ALTER TABLE tablename DROP COLUMN column_name;
```

Example:
```sql
ALTER TABLE emp DROP COLUMN phone;
```

---

### 15. How do you insert data into only specific columns of a table?

```sql
INSERT INTO tablename (col1, col2) VALUES (val1, val2);
```

---


