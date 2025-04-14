
# 📘 DBMS Experiment 5

## 🧪 Aim:
To understand and implement the use of `ORDER BY`, `GROUP BY`, `HAVING`, `ANY`, `ALL`, `EXISTS`, and `LIKE` clauses in SQL.

---

## 📚 Theory & Concepts:

### 🔹 ORDER BY
- Sorts result set in ascending (ASC) or descending (DESC) order.
```sql
SELECT * FROM Customers ORDER BY CustomerName ASC;
SELECT * FROM Customers ORDER BY CustomerName DESC;
```

---

### 🔹 GROUP BY
- Groups rows with same values.
- Used with aggregate functions like `COUNT()`, `AVG()`, etc.
```sql
SELECT DNO, COUNT(*), AVG(SALARY)
FROM EMPLOYEE
GROUP BY DNO;
```

---

### 🔹 HAVING
- Applies conditions to grouped results (like WHERE for groups).
```sql
SELECT PNUMBER, PNAME, COUNT(*)
FROM PROJECT, WORKS_ON
WHERE PNUMBER = PNO
GROUP BY PNUMBER, PNAME
HAVING COUNT(*) > 2;
```

---

### 🔹 ANY / ALL
- `ANY`: True if any subquery value satisfies the condition.  
- `ALL`: True only if all values satisfy the condition.
```sql
SELECT * FROM faculty
WHERE dno < ANY (SELECT dno FROM dept WHERE budget < 10000);

SELECT * FROM faculty
WHERE dno < ALL (SELECT dno FROM dept WHERE budget < 10000);
```

---

### 🔹 EXISTS / NOT EXISTS
- Checks for existence of rows returned by a subquery.
```sql
SELECT name, dno
FROM faculty
WHERE EXISTS (
  SELECT dno FROM dept
  WHERE faculty.dno = dept.dno AND budget > 7000
);
```

---

### 🔹 LIKE
- Used for pattern matching with `%` (any number of characters) and `_` (single character).
```sql
SELECT FNAME, LNAME
FROM EMPLOYEE
WHERE ADDRESS LIKE '%Houston,TX%';
```

---

## 💻 SQL Code (copy and paste this block into MySQL Workbench):

```sql
-- Create tables
CREATE DATABASE IF NOT EXISTS DBMS_EXP5;
USE DBMS_EXP5;

CREATE TABLE dept (
    dno INT PRIMARY KEY,
    dname VARCHAR(50),
    budget INT
);

CREATE TABLE faculty (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    salary INT,
    experience INT,
    dno INT,
    FOREIGN KEY (dno) REFERENCES dept(dno)
);

-- Insert sample data
INSERT INTO dept VALUES (1, 'CSE', 8000), (2, 'AIML', 9000), (3, 'ECE', 6000), (4, 'IT', 12000);

INSERT INTO faculty VALUES 
(101, 'Alice', 5500, 4, 1),
(102, 'Sam', 4800, 2, 2),
(103, 'John', 7200, 6, 3),
(104, 'Annah', 5000, 3, 1),
(105, 'Sanjay', 6200, 5, 2),
(106, 'Gaurav', 4700, 4, 3),
(107, 'Aaron', 8000, 7, 4),
(108, 'Gitesh', 5100, 2, 1);

-- Queries
-- 1. ID, Name, Salary in increasing order of salary
SELECT id, name, salary FROM faculty ORDER BY salary ASC;

-- 2. ID, Name, Salary in decreasing order of experience
SELECT id, name, salary FROM faculty ORDER BY experience DESC;

-- 3. ID, Name, Salary in increasing salary & decreasing experience
SELECT id, name, salary FROM faculty ORDER BY salary ASC, experience DESC;

-- 4. Average experience department-wise
SELECT dno, AVG(experience) AS avg_experience FROM faculty GROUP BY dno;

-- 5. Maximum salary department-wise
SELECT dno, MAX(salary) AS max_salary FROM faculty GROUP BY dno;

-- 6. Avg salary per department > 5000
SELECT dno, AVG(salary) AS avg_salary
FROM faculty
GROUP BY dno
HAVING AVG(salary) > 5000;

-- 7. Faculty names:
-- a) Starting with 'S'
SELECT * FROM faculty WHERE name LIKE 'S%';

-- b) Ending with 'n'
SELECT * FROM faculty WHERE name LIKE '%n';

-- c) Starting with 'A' and ending with 'h'
SELECT * FROM faculty WHERE name LIKE 'A%h';

-- d) Must contain 'a'
SELECT * FROM faculty WHERE name LIKE '%a%';

-- e) 5-letter names starting with 'g'
SELECT * FROM faculty WHERE name LIKE 'g____';

-- 8. Use of ANY clause
SELECT name, dno FROM faculty
WHERE dno < ANY (SELECT dno FROM dept WHERE budget < 10000);

-- 9. Use of ALL clause
SELECT name, dno FROM faculty
WHERE dno < ALL (SELECT dno FROM dept WHERE budget < 10000);

-- 10. EXISTS
SELECT name, dno FROM faculty
WHERE EXISTS (
  SELECT dno FROM dept WHERE faculty.dno = dept.dno AND budget > 7000
);

-- 11. NOT EXISTS
SELECT name, dno FROM faculty
WHERE NOT EXISTS (
  SELECT dno FROM dept WHERE faculty.dno = dept.dno AND budget > 7000
);

-- 12. Faculty who work in department AIML
SELECT name FROM faculty
WHERE dno = (SELECT dno FROM dept WHERE dname = 'AIML');
```

---

## 🎯 Learning Outcomes:
- Understood sorting data using `ORDER BY`.
- Learned data grouping and aggregation using `GROUP BY`, `HAVING`.
- Practiced subqueries using `ANY`, `ALL`, `EXISTS`.
- Explored pattern matching with `LIKE`.

---

## ❓ Viva Questions with Answers:

1. **What is the purpose of `ORDER BY` in SQL?**  
   ➤ It sorts the result set in ascending or descending order.

2. **What is the default sorting order in SQL?**  
   ➤ Ascending (`ASC`).

3. **How to sort records in descending order?**  
   ➤ Use `ORDER BY column_name DESC`.

4. **Why do we use `GROUP BY`?**  
   ➤ To group rows with the same values and apply aggregate functions.

5. **Can we use `GROUP BY` without aggregate functions?**  
   ➤ Yes, but it's typically used with them.

6. **What’s the difference between `WHERE` and `HAVING`?**  
   ➤ `WHERE` filters rows, `HAVING` filters groups.

7. **What does `COUNT(*)` return?**  
   ➤ Total number of rows.

8. **What is the purpose of `AVG()`?**  
   ➤ Returns the average value.

9. **What is `ANY` used for?**  
   ➤ Checks if *any* value in a subquery satisfies a condition.

10. **What does `ALL` do?**  
    ➤ Returns true only if *all* values satisfy the condition.

11. **What is a subquery?**  
    ➤ A query inside another query.

12. **Difference between `IN` and `EXISTS`?**  
    ➤ `IN` checks for value presence; `EXISTS` checks for row existence.

13. **How does `LIKE` work?**  
    ➤ Used for pattern matching in strings.

14. **What does `%` represent in LIKE?**  
    ➤ Any number of characters.

15. **What does `_` mean in LIKE?**  
    ➤ A single character.

16. **Can `HAVING` be used without `GROUP BY`?**  
    ➤ Not typically. It’s designed for use with groups.

17. **Can we use aggregate functions in `WHERE` clause?**  
    ➤ No, use `HAVING` for that.

18. **What is a foreign key?**  
    ➤ A field in one table that refers to the primary key in another.

19. **Purpose of `EXISTS` clause?**  
    ➤ Checks if the subquery returns any rows.

20. **What does `NOT EXISTS` do?**  
    ➤ Returns true if the subquery returns no rows.

21. **What is the result of `MAX(salary)`?**  
    ➤ Highest salary value.

22. **Use of aliases in SQL?**  
    ➤ To rename columns or tables for readability.

23. **What is a composite key?**  
    ➤ A primary key made of multiple columns.

24. **Can we sort by multiple columns?**  
    ➤ Yes, using `ORDER BY col1 ASC, col2 DESC`.

25. **How do subqueries improve SQL?**  
    ➤ Enable complex filtering and dynamic data lookup.

---
