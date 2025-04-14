# 🧪 Experiment 4 – Aggregate & Built-in Functions

## 🎯 Aim:

Implement SQL queries using aggregate functions (SUM, AVG, MIN, MAX, COUNT) and built-in functions (ASCII, ABS, CONCAT, SUBSTR, TRIM, UPPER, LOWER, COS, SIN, TAN, LOG, POWER, ROUND, FLOOR, CEIL, SQRT, and date functions) on a faculty table.

Faculty schema:

faculty(fid, name, dob, exp, no_of_awards, dno, sal, address, phone)

---

## 💻 SQL Code

Paste the entire block below into MySQL Workbench:

```sql
-- Creating the faculty table
CREATE TABLE faculty (
  fid INT,
  name VARCHAR(50),
  dob DATE,
  exp INT,
  no_of_awards INT,
  dno INT,
  sal DECIMAL(10,2),
  address VARCHAR(100),
  phone VARCHAR(15)
);

-- 1. Sum of all salaries
SELECT SUM(sal) AS total_salary FROM faculty;

-- 2. Sum of salaries for dept no. 1
SELECT SUM(sal) AS dept1_total_salary FROM faculty WHERE dno = 1;

-- 3. Average, Min, Max salary
SELECT AVG(sal) AS avg_salary, MIN(sal) AS min_salary, MAX(sal) AS max_salary FROM faculty;

-- 4. Average, Min, Max salary for dept 4
SELECT AVG(sal) AS avg_salary_d4, MIN(sal) AS min_salary_d4, MAX(sal) AS max_salary_d4 
FROM faculty WHERE dno = 4;

-- 5. Average experience for dept 1
SELECT AVG(exp) AS avg_exp_d1 FROM faculty WHERE dno = 1;

-- 6. Count of faculties in college
SELECT COUNT(*) AS total_faculty FROM faculty;

-- 7. Count of faculties in dept no. 2
SELECT COUNT(*) AS dept2_faculty_count FROM faculty WHERE dno = 2;

-- 8. Built-in function demonstration
SELECT 
  ASCII('A') AS ascii_val, 
  ABS(-5) AS abs_val, 
  CONCAT('Moin', 'AI') AS full_name, 
  SUBSTR('AI-DS', 1, 2) AS substr_result, 
  TRIM('   Hello   ') AS trimmed_text, 
  UPPER('hello') AS upper_text, 
  LOWER('HELLO') AS lower_text,
  COS(0) AS cos_val, 
  SIN(0) AS sin_val, 
  TAN(0) AS tan_val, 
  LOG(10) AS log_val, 
  POWER(2,3) AS power_val, 
  ROUND(3.145) AS rounded_val, 
  FLOOR(4.9) AS floor_val, 
  CEIL(4.1) AS ceil_val, 
  SQRT(16) AS sqrt_val;

-- 9. Date functions (demonstration using current date)
SELECT 
  CURDATE() AS today,
  NOW() AS current_time,
  DAY(CURDATE()) AS day_val,
  MONTH(CURDATE()) AS month_val,
  YEAR(CURDATE()) AS year_val;
```

---

## 📘 Theory

| Function     | Purpose                                                       |
|--------------|---------------------------------------------------------------|
| COUNT()      | Returns number of rows.                                       |
| SUM()        | Returns total value of a numeric column.                      |
| AVG()        | Returns average value.                                        |
| MIN()        | Returns minimum value.                                        |
| MAX()        | Returns maximum value.                                        |
| ASCII()      | Returns ASCII value of a character.                           |
| SUBSTRING()  | Extracts characters from a string.                            |
| TRIM()       | Removes leading and trailing spaces.                          |
| UPPER()      | Converts string to uppercase.                                 |
| LOWER()      | Converts string to lowercase.                                 |
| CONCAT()     | Concatenates multiple strings.                                |
| ABS()        | Returns absolute value.                                       |
| COS(), SIN(), TAN() | Trigonometric functions.                             |
| LOG()        | Returns natural logarithm.                                    |
| POWER(x, y)  | Returns x^y.                                                  |
| ROUND()      | Rounds to nearest whole number.                               |
| FLOOR()      | Rounds down.                                                  |
| CEIL()       | Rounds up.                                                    |
| SQRT()       | Returns square root.                                          |

---
---
---
---
---
---
---
---
---
---
## 🎤 Viva Questions and Answers

1. ❓ What is the purpose of aggregate functions in SQL?  
   ✅ Aggregate functions perform calculations on multiple rows of a table and return a single result, e.g., SUM, AVG, MIN, MAX, COUNT.

2. ❓ What does the SUM() function do?  
   ✅ SUM() adds up all the numeric values in a specified column.

3. ❓ How is the AVG() function different from SUM()?  
   ✅ AVG() returns the average (mean) value, while SUM() returns the total.

4. ❓ What is the purpose of COUNT()?  
   ✅ COUNT() returns the number of rows that match a condition.

5. ❓ How do you find the highest salary in a table?  
   ✅ By using SELECT MAX(sal) FROM faculty;

6. ❓ What is the use of the MIN() function?  
   ✅ MIN() returns the smallest value from a column.

7. ❓ What is the output of COUNT(*) and COUNT(column_name)?  
   ✅ COUNT(*) counts all rows; COUNT(column_name) counts non-null values in that column.

8. ❓ What does the ASCII() function do?  
   ✅ It returns the ASCII code of the first character in a string.

9. ❓ What is the output of ASCII('A')?  
   ✅ 65

10. ❓ What is the use of ABS() in SQL?  
    ✅ ABS() returns the absolute (positive) value of a number.

11. ❓ How is CONCAT() used in SQL?  
    ✅ CONCAT() joins two or more strings together. Example: CONCAT('Hello', 'World') → HelloWorld

12. ❓ What does SUBSTR() or SUBSTRING() do?  
    ✅ It extracts a part of a string starting from a specified position.

13. ❓ How does the TRIM() function help?  
    ✅ TRIM() removes extra spaces from the beginning and end of a string.

14. ❓ What is the output of UPPER('hello')?  
    ✅ HELLO

15. ❓ What is the use of LOWER() in SQL?  
    ✅ It converts all characters in a string to lowercase.

16. ❓ What does COS(0), SIN(0), and TAN(0) return?  
    ✅ COS(0) = 1, SIN(0) = 0, TAN(0) = 0

17. ❓ What does the LOG() function return in SQL?  
    ✅ LOG() returns the natural logarithm (base e) of a number.

18. ❓ What is POWER(2,3) in SQL?  
    ✅ It returns 8 (2 raised to the power of 3).

19. ❓ What is the difference between FLOOR() and CEIL()?  
    ✅ FLOOR() rounds down to the nearest integer, CEIL() rounds up.

20. ❓ What does ROUND(3.145) return?  
    ✅ It returns 3 (depending on default precision; can also round to specific decimals).

21. ❓ How do you calculate square root in SQL?  
    ✅ Using SQRT(). Example: SQRT(16) returns 4.

22. ❓ What are date functions in SQL?  
    ✅ Functions that extract or manipulate date values, e.g., CURDATE(), NOW(), YEAR(), MONTH(), DAY().

23. ❓ What is the difference between CURDATE() and NOW()?  
    ✅ CURDATE() returns only the date, NOW() returns date and current time.

24. ❓ How do you extract the month from a date column?  
    ✅ Using MONTH(date_column) function.

25. ❓ Can we use aggregate functions with WHERE clause?  
    ✅ Yes, but only before aggregation. To filter after aggregation, use HAVING clause.
