
# Experiment 9 – Cursor to Retrieve Top 5 Highest-Paid Employees

## Aim:
To write a cursor to retrieve the top five highest-paid employees from the EMPLOYEE table.

---

## Theory:

To retrieve the top five highest-paid employees from the EMPLOYEE table using a cursor, the following processes are followed:

1. **Query Design:**
   A SQL query is constructed to select employee records ordered by salary in descending order. This brings the highest-paid employees to the top.

2. **Cursor Declaration:**
   A cursor is declared to encapsulate this query. It allows row-by-row processing of the result set.

3. **Variable Initialization:**
   Variables are declared to temporarily store each row’s data such as EmpNo, Name, Salary, Designation, and DeptID.

4. **Open and Iterate Cursor:**
   The cursor is opened and a loop is used to fetch and process only the first five rows using a counter.

5. **Data Processing:**
   The retrieved data can be printed or used for further operations like storing into another table.

6. **Close Cursor:**
   Once the required rows are processed, the cursor is closed to free up resources.

---

## SQL Code:
(You can directly paste this into MySQL Workbench and change names/IDs for different runs.)

```sql
-- Create EMP table
CREATE TABLE EMP (
  EmpNo INT PRIMARY KEY,
  Name VARCHAR(50),
  Salary DECIMAL(10,2),
  Designation VARCHAR(50),
  DeptID INT
);

-- Insert sample data
INSERT INTO EMP VALUES
(101, 'Amit', 90000.00, 'Manager', 10),
(102, 'Nina', 87000.00, 'Tech Lead', 20),
(103, 'Rahul', 92000.00, 'Architect', 30),
(104, 'Priya', 95000.00, 'Manager', 40),
(105, 'Karan', 89000.00, 'Developer', 10),
(106, 'Anjali', 91000.00, 'Analyst', 20),
(107, 'Rohan', 88000.00, 'Developer', 30),
(108, 'Sneha', 86000.00, 'Tester', 40);

-- Cursor block to display top 5 highest-paid employees
DELIMITER $$

CREATE PROCEDURE TopFiveHighestPaidEmployees()
BEGIN
  DECLARE done INT DEFAULT 0;
  DECLARE v_EmpNo INT;
  DECLARE v_Name VARCHAR(50);
  DECLARE v_Salary DECIMAL(10,2);
  DECLARE v_Designation VARCHAR(50);
  DECLARE v_DeptID INT;
  DECLARE counter INT DEFAULT 0;

  DECLARE cur CURSOR FOR
    SELECT EmpNo, Name, Salary, Designation, DeptID
    FROM EMP
    ORDER BY Salary DESC;

  DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = 1;

  OPEN cur;

  read_loop: LOOP
    FETCH cur INTO v_EmpNo, v_Name, v_Salary, v_Designation, v_DeptID;

    IF done = 1 OR counter = 5 THEN
      LEAVE read_loop;
    END IF;

    -- Displaying output (in actual use, you might insert into another table or print)
    SELECT v_EmpNo AS EmpNo, v_Name AS Name, v_Salary AS Salary, v_Designation AS Designation, v_DeptID AS DeptID;

    SET counter = counter + 1;
  END LOOP;

  CLOSE cur;
END$$

DELIMITER ;

-- Call the procedure
CALL TopFiveHighestPaidEmployees();
```

---

## Learning Outcomes:

- Understand the usage of cursors in SQL for row-wise data processing.
- Learn how to retrieve a specific number of rows from a sorted result set.
- Gain hands-on practice on declaring and using cursors in stored procedures.
- Understand resource management with opening and closing cursors.

---

## Viva Questions (with Answers):

1. **What is a cursor in SQL?**  
   A cursor is a database object used to retrieve and process rows returned by a query one at a time.

2. **Why do we need cursors when we have SQL queries?**  
   Cursors allow row-wise operations and are useful when we need to process individual rows differently.

3. **What are the types of cursors?**  
   Implicit cursors (automatically created for DML operations) and explicit cursors (declared and controlled by the user).

4. **How do you declare a cursor?**  
   Using the syntax: `DECLARE cursor_name CURSOR FOR SELECT ...;`

5. **What is a cursor loop?**  
   A loop that fetches data from a cursor row-by-row using FETCH and processes it.

6. **What is the importance of closing a cursor?**  
   Closing releases the memory and system resources associated with the cursor.

7. **What happens if you forget to close a cursor?**  
   It may lead to memory leaks and degrade database performance.

8. **What is a handler in SQL?**  
   A handler deals with conditions like NOT FOUND or SQL exceptions during cursor operations.

9. **What is the default cursor type in MySQL?**  
   Forward-only cursors that can be read once from start to end.

10. **Can you use cursors in functions?**  
    No, cursors are generally used in stored procedures, not functions.

11. **Can we update records using a cursor?**  
    Yes, by using a cursor with the FOR UPDATE clause and performing an update within the loop.

12. **What is the maximum number of rows a cursor can fetch?**  
    There is no defined limit, but memory and performance constraints apply.

13. **How do you detect the end of a cursor’s result set?**  
    Using the `NOT FOUND` condition and a handler.

14. **Can cursors be nested?**  
    Yes, but nesting cursors increases complexity and should be avoided unless necessary.

15. **What is a read-only cursor?**  
    A cursor that cannot be used to update the rows it fetches.

16. **Can we use cursors in triggers?**  
    Generally not recommended as it can lead to performance issues and recursion.

17. **What are alternatives to cursors?**  
    Set-based operations using joins and subqueries are often more efficient.

18. **Are cursors faster than normal SQL queries?**  
    No, cursors are slower due to row-wise processing.

19. **How is a cursor different from a loop?**  
    Cursor is used specifically for data retrieval row-by-row, loop is a generic control structure.

20. **What is FETCH in cursor?**  
    FETCH retrieves the next row from the result set into variables.

21. **How many cursors can be opened at a time?**  
    It depends on the DBMS, but multiple cursors can be opened if resources allow.

22. **What is a scrollable cursor?**  
    A cursor that allows movement in both forward and backward directions.

23. **What is cursor FOR loop?**  
    A simplified way of looping through a cursor without explicit open/fetch/close.

24. **What is a parameterized cursor?**  
    A cursor that accepts parameters to dynamically filter the result set.

25. **Why use stored procedure with cursor?**  
    It allows encapsulating logic that can be reused and maintained easily.

---
