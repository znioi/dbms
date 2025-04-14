Here's a complete README.md for your GitHub repository containing Experiment 2 (DDL & DML) using MySQL Workbench.

Feel free to copy this and place it inside your exp2-dbms repository:

📁 README.md

# 💾 DBMS Experiment 2 – DDL and DML Queries (MySQL Workbench)

This repository contains practical and viva material for Experiment 2 of the DBMS lab course. It includes hands-on exercises using Data Definition Language (DDL) and Data Manipulation Language (DML) SQL queries in MySQL Workbench.

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

Would you like me to now generate viva questions based on this experiment?
