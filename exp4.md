# 📘 DBMS Experiment 4

## 🧪 Aim:
To demonstrate the use of aggregate functions (`SUM`, `AVG`, `MIN`, `MAX`, `COUNT`) and built-in string, mathematical, and date functions in SQL using a faculty schema.

---

## 🧠 Theory

### 🔹 Aggregate Functions:
- **`COUNT()`**: Counts number of rows.
- **`SUM()`**: Adds all values in a column.
- **`AVG()`**: Calculates average of a column.
- **`MIN()` / `MAX()`**: Finds lowest/highest value.

### 🔹 String Functions:
- **`ASCII(c)`**: ASCII value of character `c`.
- **`SUBSTRING(s, i, n)`**: Extracts `n` characters from `s` starting at index `i`.
- **`TRIM(s)`**: Removes leading/trailing spaces.
- **`UPPER(s)` / `LOWER(s)`**: Converts string to uppercase/lowercase.
- **`CONCAT(s1, s2, ...)`**: Combines strings.

### 🔹 Math Functions:
- **`ABS(x)`**: Absolute value.
- **`COS(x)`, `SIN(x)`, `TAN(x)`**: Trigonometric functions.
- **`LOG(x)`**: Natural logarithm.
- **`POWER(x, y)`**: x raised to the power y.
- **`ROUND(x, d)`**: Rounds to `d` decimals.
- **`FLOOR(x)`**: Rounds down.
- **`CEIL(x)`**: Rounds up.
- **`SQRT(x)`**: Square root.

### 🔹 Date Functions (examples):
- `CURDATE()`, `NOW()`, `YEAR()`, `MONTH()`, `DATEDIFF()`

---

## 💻 SQL Code (Paste this into MySQL Workbench):

```sql
-- Create and use database
CREATE DATABASE IF NOT EXISTS DBMS_EXP4;
USE DBMS_EXP4;

-- Faculty Table
CREATE TABLE faculty (
    fid INT PRIMARY KEY,
    name VARCHAR(50),
    dob DATE,
    exp INT,
    no_of_awards INT,
    dno INT,
    sal INT,
    address VARCHAR(100),
    phone VARCHAR(15)
);

-- Insert sample data
INSERT INTO faculty VALUES 
(1, 'Alice', '1985-05-15', 12, 3, 1, 6000, 'Hyd', '9999990001'),
(2, 'Bob', '1990-08-10', 7, 2, 2, 5500, 'Delhi', '9999990002'),
(3, 'Charlie', '1980-03-20', 15, 4, 4, 8000, 'Chennai', '9999990003'),
(4, 'David', '1992-11-01', 5, 1, 1, 5000, 'Mumbai', '9999990004'),
(5, 'Eva', '1988-09-25', 9, 2, 3, 6500, 'Pune', '9999990005');

-- 1. Total salary of all faculties
SELECT SUM(sal) AS total_salary FROM faculty;

-- 2. Total salary of faculties in dept no. 1
SELECT SUM(sal) AS dept1_total_salary FROM faculty WHERE dno = 1;

-- 3. Average, Min, Max salary of all faculties
SELECT AVG(sal) AS avg_salary, MIN(sal) AS min_salary, MAX(sal) AS max_salary FROM faculty;

-- 4. Average, Min, Max salary of faculties in dept no. 4
SELECT AVG(sal) AS avg_salary, MIN(sal) AS min_salary, MAX(sal) AS max_salary 
FROM faculty WHERE dno = 4;

-- 5. Average experience of faculties in dept no. 1
SELECT AVG(exp) AS avg_exp FROM faculty WHERE dno = 1;

-- 6. Total number of faculties in college
SELECT COUNT(*) AS total_faculties FROM faculty;

-- 7. Number of faculties in dept no. 2
SELECT COUNT(*) AS dept2_faculties FROM faculty WHERE dno = 2;

-- 8. String/Math Functions
SELECT 
    ASCII('A') AS ascii_value,
    ABS(-99) AS absolute,
    CONCAT(name, ' - Faculty') AS concatenated,
    SUBSTRING(name, 1, 3) AS substringed,
    TRIM('  Hello  ') AS trimmed,
    UPPER(name) AS uppercased,
    LOWER(name) AS lowercased,
    COS(0) AS cosine,
    SIN(0) AS sine,
    TAN(0) AS tangent,
    LOG(10) AS log_value,
    POWER(2, 5) AS power_value,
    ROUND(3.14159, 2) AS rounded,
    FLOOR(3.9) AS floored,
    CEIL(3.1) AS ceiled,
    SQRT(25) AS square_root
FROM faculty LIMIT 1;

-- 9. Date Functions
SELECT 
    CURDATE() AS today,
    NOW() AS now_time,
    YEAR(dob) AS birth_year,
    MONTH(dob) AS birth_month,
    DATEDIFF(CURDATE(), dob) AS days_alive
FROM faculty;
```

---

## 🎯 Learning Outcomes:
- Understood the working of SQL aggregate functions.
- Learned how to perform string and math operations using built-in functions.
- Practiced using various date-related functions.
- Developed the ability to analyze and manipulate tabular data using SQL.

---

## ❓ Viva Questions with Answers

1. **What does `SUM()` do in SQL?**  
   ➤ It adds up all values in a specified column.

2. **What is the use of `AVG()`?**  
   ➤ It returns the average value of a numeric column.

3. **How to count number of records in a table?**  
   ➤ Use `SELECT COUNT(*) FROM table_name;`.

4. **What does `MIN()` and `MAX()` return?**  
   ➤ Minimum and maximum value in a column respectively.

5. **How to find number of faculties in dept 1?**  
   ➤ `SELECT COUNT(*) FROM faculty WHERE dno = 1;`.

6. **How does `ASCII()` work?**  
   ➤ Returns the ASCII value of the first character.

7. **What is the output of `ABS(-5)`?**  
   ➤ `5` (absolute value).

8. **What does `CONCAT('A', 'B')` return?**  
   ➤ `AB`.

9. **What is `SUBSTRING('Hello', 1, 3)`?**  
   ➤ `Hel`.

10. **What is the difference between `TRIM` and `SUBSTRING`?**  
    ➤ `TRIM` removes spaces, `SUBSTRING` extracts part of string.

11. **Difference between `UPPER()` and `LOWER()`?**  
    ➤ `UPPER()` converts to capital, `LOWER()` to small letters.

12. **What is `COS(0)`?**  
    ➤ `1`.

13. **What does `LOG(10)` return?**  
    ➤ Natural logarithm of 10.

14. **What does `POWER(2, 3)` return?**  
    ➤ `8`.

15. **How does `ROUND()` work?**  
    ➤ Rounds a number to specified decimal places.

16. **How does `FLOOR()` and `CEIL()` differ?**  
    ➤ `FLOOR()` rounds down, `CEIL()` rounds up.

17. **Use of `SQRT(25)`?**  
    ➤ Returns `5`.

18. **What is the result of `NOW()`?**  
    ➤ Current date and time.

19. **How to get only the year from a date?**  
    ➤ Use `YEAR(dob)`.

20. **Which function gives current date?**  
    ➤ `CURDATE()`.

21. **How to find days between two dates?**  
    ➤ Use `DATEDIFF(date1, date2)`.

22. **Why do we use built-in functions in SQL?**  
    ➤ To manipulate and analyze data easily.

23. **Can aggregate functions be used in `WHERE` clause?**  
    ➤ No, use `HAVING` instead.

24. **Is it mandatory to use `GROUP BY` with aggregate functions?**  
    ➤ No, only when grouping is needed.

25. **What’s the output of `TRIM(' Hello ')`?**  
    ➤ `'Hello'`.

---
