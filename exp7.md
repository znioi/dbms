
# Experiment 7 - Implementing Various JOIN Operations (INNER, LEFT, RIGHT)

---

## 🎯 Aim
To implement and understand various SQL JOIN operations — specifically `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`.

---

## 📚 Theory

### 🔹 INNER JOIN
Returns only those records that have matching values in both tables.
```sql
SELECT * 
FROM TableA 
INNER JOIN TableB 
ON TableA.id = TableB.id;
```

### 🔹 LEFT JOIN (LEFT OUTER JOIN)
Returns all records from the left table and matched records from the right table.
```sql
SELECT * 
FROM TableA 
LEFT JOIN TableB 
ON TableA.id = TableB.id;
```

### 🔹 RIGHT JOIN (RIGHT OUTER JOIN)
Returns all records from the right table and matched records from the left table.
```sql
SELECT * 
FROM TableA 
RIGHT JOIN TableB 
ON TableA.id = TableB.id;
```

---

## 🧪 SQL Code (Single Block for SQL Workbench)

```sql
CREATE TABLE Student(
  Roll_no INT PRIMARY KEY,
  Name VARCHAR(10) UNIQUE,
  Address VARCHAR(20),
  Phone VARCHAR(15),
  Age INT NOT NULL
);

CREATE TABLE Course(
  Course_id INT PRIMARY KEY,
  C_name VARCHAR(10)
);

CREATE TABLE StudentCourse(
  Course_id INT,
  Roll_no INT,
  FOREIGN KEY (Course_id) REFERENCES Course(Course_id),
  FOREIGN KEY (Roll_no) REFERENCES Student(Roll_no)
);

INSERT INTO Student (Roll_no, Name, Address, Phone, Age) VALUES 
(1, 'Aanchal', 'Lucknow', '6754386755', 20),
(2, 'Aman', 'Aligarh', '8375913020', 21),
(3, 'Moin', 'Delhi', '7680002345', 19),
(4, 'Tanuj', 'Raipur', '7586901234', 19),
(5, 'Drishti', 'Jaipur', '6749300021', 20),
(6, 'Prem', 'Mathura', '9078564567', 21),
(7, 'Aditya', 'Sitapur', '7856901028', 18),
(8, 'Lakshya', 'Dehradun', '7895693456', 19);

INSERT INTO Course (Course_id, C_name) VALUES 
(1, 'AIML'),
(2, 'AIDS'),
(3, 'IIOT'),
(4, 'CSE'),
(5, 'IT');

INSERT INTO StudentCourse (Course_id, Roll_no) VALUES 
(1, 1),
(2, 2),
(1, 5),
(2, 3),
(3, 4),
(4, 9),
(5, 10),
(4, 11);

-- INNER JOIN
SELECT StudentCourse.Course_id, Student.Name, Student.Age
FROM Student 
INNER JOIN StudentCourse 
ON Student.Roll_no = StudentCourse.Roll_no;

-- LEFT JOIN
SELECT Student.Name, StudentCourse.Course_id
FROM Student 
LEFT JOIN StudentCourse 
ON Student.Roll_no = StudentCourse.Roll_no;

-- RIGHT JOIN
SELECT Student.Name, StudentCourse.Course_id
FROM StudentCourse 
RIGHT JOIN Student 
ON Student.Roll_no = StudentCourse.Roll_no;

-- WHERE JOIN
SELECT Student.Name, Student.Address
FROM Student, StudentCourse 
WHERE Student.Roll_no = StudentCourse.Roll_no 
AND StudentCourse.Course_id = 3;

SELECT Student.Name, Student.Phone
FROM Student, StudentCourse 
WHERE Student.Roll_no = StudentCourse.Roll_no 
AND StudentCourse.Course_id = 2 
AND Student.Age = 20;

-- JOIN with three tables
SELECT Student.Name, Student.Age, StudentCourse.Course_id, Course.C_name
FROM Student, StudentCourse, Course 
WHERE Student.Roll_no = StudentCourse.Roll_no 
AND StudentCourse.Course_id = Course.Course_id;

SELECT Student.Name, Student.Age
FROM Student, StudentCourse, Course 
WHERE Student.Roll_no = StudentCourse.Roll_no 
AND StudentCourse.Course_id = Course.Course_id 
AND Course.C_name = 'AIDS';
```

---

## ✅ Learning Outcomes
- Understood how JOINs combine rows from two or more tables.
- Applied INNER, LEFT, RIGHT JOINs to extract useful relational data.
- Learned how to filter JOINed results using WHERE clauses.
- Gained practical exposure to using JOINs with multiple tables.

---

## 🎤 Viva Questions (with Answers)

1. **What is a JOIN in SQL?**  
   A JOIN clause is used to combine rows from two or more tables based on a related column between them.

2. **What is the default JOIN in SQL?**  
   The default JOIN is the INNER JOIN.

3. **What is the difference between INNER and OUTER JOIN?**  
   INNER JOIN returns only matched records. OUTER JOIN returns matched and unmatched records depending on LEFT, RIGHT, or FULL.

4. **What does LEFT JOIN return?**  
   All records from the left table and matched records from the right table. Nulls for unmatched right-side rows.

5. **What does RIGHT JOIN return?**  
   All records from the right table and matched records from the left table.

6. **How is FULL OUTER JOIN different?**  
   Returns all matched and unmatched records from both tables.

7. **Can we use WHERE clause with JOIN?**  
   Yes, WHERE can be used to filter results after the JOIN is performed.

8. **What is the syntax for INNER JOIN?**  
   SELECT * FROM A INNER JOIN B ON A.id = B.id;

9. **Can we join more than two tables?**  
   Yes, you can join any number of tables using multiple JOIN clauses.

10. **Why do we use aliases in JOINs?**  
    To simplify table names and make SQL queries more readable.

11. **What happens if the JOIN condition is incorrect?**  
    It may return incorrect or no results.

12. **Can we perform JOIN without a foreign key?**  
    Yes, but it’s not recommended as it may lead to inconsistent data.

13. **What is a CROSS JOIN?**  
    A CROSS JOIN returns the Cartesian product of two tables.

14. **What is a SELF JOIN?**  
    A SELF JOIN is a regular join but the table is joined with itself.

15. **Can we use GROUP BY with JOIN?**  
    Yes, JOINs can be combined with GROUP BY for aggregated results.

16. **How do we fetch students enrolled in a specific course?**  
    Use JOIN with a WHERE clause filtering Course.Course_id.

17. **What is NULL in JOIN context?**  
    It indicates no match found on the joined table side.

18. **Why does LEFT JOIN return NULL values?**  
    When no matching row is found in the right table.

19. **What is a primary use of RIGHT JOIN?**  
    To get all records from the second table regardless of match in the first.

20. **Which JOIN gives the largest result set?**  
    FULL OUTER JOIN and CROSS JOIN can produce large outputs.

21. **Which JOIN is fastest?**  
    INNER JOIN is typically faster due to fewer rows returned.

22. **Can we join tables using non-primary key fields?**  
    Yes, as long as the fields have meaningful relationships.

23. **What is the difference between USING and ON in JOIN?**  
    USING is used when both columns have the same name; ON allows more flexibility.

24. **Can JOINs replace subqueries?**  
    In many cases, JOINs can be used instead of subqueries and perform better.

25. **How do JOINs help in real-world DBMS?**  
    JOINs are essential to combine and query related data across multiple tables efficiently.

---

