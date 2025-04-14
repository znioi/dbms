# 🧪 DBMS Experiment 6

## 🔍 Aim
To understand and perform set operations in SQL such as `UNION`, `INTERSECT`, and `EXCEPT` using appropriate SQL queries on relational tables.

---

## 📚 Theory

### 1. UNION
- Combines results of two or more `SELECT` queries.
- Eliminates duplicates by default.
- Each `SELECT` must return the same number of columns with compatible data types.

```sql
SELECT name, age FROM table1
UNION
SELECT name, age FROM table2;
```

### 2. INTERSECT (Not direct in MySQL)
- Returns common rows between two queries.
- Can be simulated using `IN`, `EXISTS`, or `INNER JOIN`.

```sql
SELECT column1, column2
FROM table1
WHERE column1 IN (
    SELECT column1 FROM table2
);
```

### 3. EXCEPT / MINUS
- Returns rows from the first query that do not exist in the second.
- Not directly available in MySQL; can be simulated using `NOT IN`.

```sql
SELECT name, age FROM table1
WHERE (name, age) NOT IN (
  SELECT name, age FROM table2
);
```

---

## 💻 SQL Code

```sql
-- Create and use database
CREATE DATABASE IF NOT EXISTS DBMS_EXP6;
USE DBMS_EXP6;

-- Create Section Table
CREATE TABLE section (
    course_id VARCHAR(10),
    sem VARCHAR(10),
    year INT
);

-- Insert Data
INSERT INTO section VALUES 
('CS101', 'Fall', 2017),
('CS102', 'Spring', 2018),
('CS103', 'Fall', 2017),
('CS104', 'Spring', 2018),
('CS105', 'Fall', 2017),
('CS106', 'Spring', 2018),
('CS101', 'Spring', 2018);

-- 1. Courses in Fall 2017
SELECT course_id FROM section
WHERE sem = 'Fall' AND year = 2017;

-- 2. Courses in Spring 2018
SELECT course_id FROM section
WHERE sem = 'Spring' AND year = 2018;

-- 3. Courses in Fall 2017 OR Spring 2018 (UNION)
SELECT course_id FROM section WHERE sem = 'Fall' AND year = 2017
UNION
SELECT course_id FROM section WHERE sem = 'Spring' AND year = 2018;

-- 4. Courses in Fall 2017 AND Spring 2018 (INTERSECT simulation)
SELECT course_id FROM section
WHERE sem = 'Fall' AND year = 2017
AND course_id IN (
    SELECT course_id FROM section
    WHERE sem = 'Spring' AND year = 2018
);

-- 5. Courses in Fall 2017 BUT NOT in Spring 2018 (EXCEPT simulation)
SELECT course_id FROM section
WHERE sem = 'Fall' AND year = 2017
AND course_id NOT IN (
    SELECT course_id FROM section
    WHERE sem = 'Spring' AND year = 2018
);

-- 6. Courses in Spring 2018 BUT NOT in Fall 2017
SELECT course_id FROM section
WHERE sem = 'Spring' AND year = 2018
AND course_id NOT IN (
    SELECT course_id FROM section
    WHERE sem = 'Fall' AND year = 2017
);

-- Create instructor1 and instructor2 Tables
CREATE TABLE instructor1 (
    name VARCHAR(20),
    salary INT
);

CREATE TABLE instructor2 (
    name VARCHAR(20),
    salary INT
);

-- Insert Sample Data
INSERT INTO instructor1 VALUES 
('Amit', 55000),
('Priya', 72000),
('Rahul', 63000);

INSERT INTO instructor2 VALUES 
('Neha', 75000),
('Karan', 72000),
('Riya', 65000),
('Amit', 55000); -- common record for intersect test

-- 7. UNION of instructor1 and instructor2
SELECT * FROM instructor1
UNION
SELECT * FROM instructor2;

-- 8. UNION ALL (with duplicates)
SELECT * FROM instructor1
UNION ALL
SELECT * FROM instructor2;

-- 9. INTERSECT simulation using IN
SELECT * FROM instructor1
WHERE (name, salary) IN (
    SELECT name, salary FROM instructor2
);

-- 10. EXCEPT simulation using NOT IN
SELECT * FROM instructor1
WHERE (name, salary) NOT IN (
    SELECT name, salary FROM instructor2
);

-- 11. Highest salary in instructor1
SELECT MAX(salary) AS max_salary FROM instructor1;

-- 12. Instructors with salary less than max
SELECT * FROM instructor1
WHERE salary < (
    SELECT MAX(salary) FROM instructor1
);
```

---

## 🎯 Learning Outcomes

- Understood how to perform SQL operations involving set theory (`UNION`, `INTERSECT`, `EXCEPT`).
- Learned the use of subqueries and conditional clauses (`IN`, `NOT IN`) for simulating unsupported operations.
- Gained hands-on experience in query formulation and analysis over structured datasets.

---

## ❓ Viva Questions (with Answers)

1. **What is the purpose of the UNION operator in SQL?**  
   → Combines results of two `SELECT` queries and removes duplicates.

2. **What is the difference between UNION and UNION ALL?**  
   → `UNION` removes duplicates, `UNION ALL` retains them.

3. **Does SQL have a direct INTERSECT operator?**  
   → No, but it can be simulated using `IN`, `EXISTS`, or `JOIN`.

4. **What does the EXCEPT operator do?**  
   → Returns records from the first query not present in the second.

5. **How can you simulate INTERSECT in MySQL?**  
   → Using `IN` with subqueries or `JOIN` on matching fields.

6. **What is the condition for using UNION?**  
   → All queries must have the same number of columns and data types.

7. **What happens if the columns in a UNION don’t match?**  
   → An error is thrown due to data type or column count mismatch.

8. **Can you use ORDER BY in a UNION query?**  
   → Yes, but only after the final SELECT block.

9. **How do you find courses common to two semesters?**  
   → Use INTERSECT logic: check if course_id exists in both semesters.

10. **What is the difference between EXCEPT and NOT IN?**  
    → Both find differences; `EXCEPT` is more set-based and clearer semantically.

11. **Can you use UNION on different tables?**  
    → Yes, if they return the same column structure and types.

12. **Which operator gives a complete dataset with duplicates?**  
    → `UNION ALL`.

13. **What is a practical use case of EXCEPT?**  
    → To find records that are outdated or no longer present.

14. **Why would INTERSECT be important in a DBMS?**  
    → To find overlap between datasets (e.g., shared courses or students).

15. **What clause do you use for filtering results in SQL?**  
    → `WHERE`.

16. **What does MAX() do in SQL?**  
    → Returns the maximum value in a column.

17. **How do you compare against the maximum salary?**  
    → Use subquery: `salary < (SELECT MAX(salary) FROM table)`.

18. **What are relational algebra equivalents of UNION/EXCEPT?**  
    → `∪` for union, `−` for except, `∩` for intersect.

19. **How can you use JOIN to simulate INTERSECT?**  
    → Perform `INNER JOIN` on common attributes.

20. **Can NULL values affect UNION results?**  
    → Yes, but NULL is treated as a distinct value unless all fields match.

21. **What is the role of DISTINCT in UNION?**  
    → `UNION` uses DISTINCT internally to eliminate duplicates.

22. **Is MINUS supported in MySQL?**  
    → No, only in Oracle. Use `NOT IN` instead.

23. **What happens if there are NULLs in EXCEPT operations?**  
    → NULLs are compared as unknowns; behavior depends on DBMS.

24. **How do you find top salaries excluding the highest?**  
    → `SELECT salary FROM table WHERE salary < (SELECT MAX(salary))`.

25. **What is the importance of data type compatibility in set operations?**  
    → Ensures safe merging of data without type mismatch errors.

---
