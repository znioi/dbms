📄 exp8.md

# 🧪 Experiment 8 – Implementation of Stored Procedures and Loops in MySQL

## 🎯 Aim

To implement stored procedures using WHILE loops and nested loops for inserting records into tables, and understand control structures in MySQL.

---

## 📚 Theory

1. ✅ Stored Procedures  
A stored procedure is a precompiled collection of one or more SQL statements stored in the database. It can be invoked using the CALL command and helps in modular programming, reuse, and abstraction.

2. 🔁 WHILE Loop in MySQL  
The WHILE loop in stored procedures is used to execute a block of statements repeatedly as long as the specified condition is true.

3. 🔁 Nested Loops  
Loops inside other loops (nested loops) are used to perform multi-level operations. In the inner loop, actions are taken for every iteration of the outer loop.

4. 🗃️ Table Creation  
A table should be created with the necessary structure (e.g., integer column, status column) before using loops to populate data.

5. ➕ MOD() Function  
MOD(x, y) returns the remainder of x divided by y. Useful in determining even/odd values (MOD(i, 2) = 0 means even).

---

## 💻 Code

```sql
-- Create and use database
CREATE DATABASE expp;
USE expp;

-- Table 1: Insert odd/even using WHILE loop
CREATE TABLE sample_table (
  i INT AUTO_INCREMENT PRIMARY KEY,
  x INT,
  odd_even VARCHAR(10)
);

DELIMITER //
CREATE PROCEDURE insert_oddeven()
BEGIN
  DECLARE i INT DEFAULT 1;
  WHILE i <= 10 DO
    INSERT INTO sample_table (x, odd_even)
    VALUES (i, IF(MOD(i, 2) = 0, 'even', 'odd'));
    SET i = i + 1;
  END WHILE;
END;
//
DELIMITER ;

CALL insert_oddeven();

-- Table 2: Nested WHILE loops
CREATE TABLE colgg (
  x INT,
  counter INT,
  type VARCHAR(10)
);

DELIMITER //
CREATE PROCEDURE InOddEven()
BEGIN
  DECLARE i INT DEFAULT 1;
  DECLARE j INT;
  DECLARE counter INT DEFAULT 0;
  DECLARE x_local INT;

  WHILE i <= 4 DO
    SET counter = counter + 1;
    INSERT INTO colgg VALUES (i*1000, counter, 'OUTER loop');

    SET j = 1;
    WHILE j <= 4 DO
      SET counter = counter + 1;
      SET x_local = j;
      INSERT INTO colgg VALUES (x_local, counter, 'inner loop');
      SET j = j + 1;
    END WHILE;

    SET i = i + 1;
  END WHILE;
END;
//
DELIMITER ;

CALL InOddEven();
```

---

## 🎤 Viva Questions & Answers

1. What is a stored procedure?  
   → A named collection of SQL statements stored in the database that can be executed using CALL.

2. What is the benefit of using stored procedures?  
   → Code reusability, modular design, and improved performance.

3. What loop types are available in MySQL procedures?  
   → WHILE, REPEAT, and LOOP constructs.

4. How do you define a WHILE loop in MySQL?  
   → WHILE condition DO … END WHILE;

5. What is the purpose of DELIMITER in MySQL procedures?  
   → To distinguish procedure body from standard SQL statements using custom delimiter (e.g., //).

6. What does MOD(i, 2) do?  
   → Returns 0 if i is even, 1 if i is odd.

7. What is the role of AUTO_INCREMENT?  
   → Automatically generates sequential integer values for primary key columns.

8. What does the IF() function do in MySQL?  
   → IF(condition, true_result, false_result) – like a ternary operator.

9. What is the difference between a WHILE and a FOR loop in MySQL?  
   → WHILE requires explicit initialization and increment; FOR is not directly supported in MySQL.

10. Can you nest loops in MySQL procedures?  
    → Yes, loops can be nested inside each other.

11. What is the difference between DECLARE and SET?  
    → DECLARE creates a variable, SET assigns a value to it.

12. How many times does the outer loop run in InOddEven()?  
    → 4 times (i from 1 to 4).

13. How many times does the inner loop run for each outer iteration?  
    → 4 times (j from 1 to 4).

14. How many total rows will be inserted into colgg table?  
    → 4 (outer) × 4 (inner) + 4 (outer header rows) = 20 rows.

15. Can you use SELECT inside a procedure?  
    → Yes, SELECT can be used like other DML commands.

16. What is the purpose of the counter variable in the second procedure?  
    → To keep track of total number of insertions/iterations.

17. Is 'x_local' mandatory in the inner loop?  
    → No, it’s used for clarity or reuse, but not mandatory.

18. How do you call a procedure in MySQL?  
    → Using CALL procedure_name();

19. What happens if you don’t set DELIMITER before a procedure?  
    → MySQL will throw an error because it misinterprets the semicolon.

20. What happens if there is a syntax error inside a procedure?  
    → It won’t be created and an error message will be shown.

21. Can you update a stored procedure?  
    → No, you need to DROP and CREATE it again.

22. How do you remove a stored procedure?  
    → DROP PROCEDURE procedure_name;

23. Can we use control structures like IF, CASE inside procedures?  
    → Yes, MySQL supports IF, CASE, WHILE, LOOP, etc.

24. Can you use procedures for table creation?  
    → Yes, but it's not a common practice.

25. What is the scope of variables declared with DECLARE inside procedures?  
    → Local to the BEGIN … END block in which they are declared.

---

## 🎓 Learning Outcome

- Understand the creation and execution of stored procedures in MySQL.
- Learn to use WHILE loops and nested loops to automate repetitive tasks.
- Perform control operations like IF, MOD, and variable handling in procedural SQL.
- Apply procedural programming techniques in SQL for batch data insertion.


