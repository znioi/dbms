
# DBMS Lab - Experiment 3

## Aim
To implement **basic SQL queries** such as `CREATE`, `INSERT`, `UPDATE`, `DELETE`, and `SELECT` for two real-world scenarios: **College** and **Banking**.

---

## Theory

In SQL (Structured Query Language), basic operations are used to interact with a relational database:

- **SELECT**: Used to retrieve data from tables.
  ```sql
  SELECT column1, column2 FROM table_name WHERE condition;
````

* **INSERT**: Used to insert new records into a table.

  ```sql
  INSERT INTO table_name VALUES (value1, value2, ...);
  ```

* **DELETE**: Removes existing records.

  ```sql
  DELETE FROM table_name WHERE condition;
  ```

* **UPDATE**: Modifies existing records.

  ```sql
  UPDATE table_name SET column1 = value1 WHERE condition;
  ```

* **GROUP BY**: Groups rows with the same values and aggregates them.

  ```sql
  SELECT column, COUNT(*) FROM table_name GROUP BY column;
  ```

* **ORDER BY**: Sorts the result-set in ascending or descending order.

  ```sql
  SELECT * FROM table_name ORDER BY column ASC|DESC;
  ```

---

## Data Types Overview

| Category    | Examples                                 |
| ----------- | ---------------------------------------- |
| Numeric     | `INT`, `FLOAT`, `DECIMAL`, `NUMBER(s,p)` |
| Character   | `CHAR(n)`, `VARCHAR(n)`, `VARCHAR2(n)`   |
| Bit/String  | `BLOB`, `CLOB`                           |
| Boolean     | `TRUE`, `FALSE`, `NULL`                  |
| Date & Time | `DATE (YYYY-MM-DD)`, `TIME (HH:MM:SS)`   |
| Timestamp   | `DATE + TIME`                            |



## 💻 Executable SQL Code (Paste Directly in MySQL Workbench)

```code 
-- College Database
CREATE DATABASE IF NOT EXISTS CollegeDB;
USE CollegeDB;

CREATE TABLE Dept (
    dno INT PRIMARY KEY,
    dname VARCHAR(50),
    budget DECIMAL(10, 2)
);

CREATE TABLE Faculty (
    fid INT PRIMARY KEY,
    name VARCHAR(50),
    dno INT,
    sal DECIMAL(10, 2),
    address VARCHAR(100),
    phone VARCHAR(15),
    dob DATE,
    exp INT,
    no_of_awards INT,
    FOREIGN KEY (dno) REFERENCES Dept(dno)
);

CREATE TABLE Student (
    sid INT PRIMARY KEY,
    name VARCHAR(50),
    dno INT,
    phone VARCHAR(15),
    dob DATE,
    address VARCHAR(100),
    sem INT,
    FOREIGN KEY (dno) REFERENCES Dept(dno)
);

CREATE TABLE Society (
    sc_id INT PRIMARY KEY,
    name VARCHAR(50)
);

CREATE TABLE Std_soc (
    sid INT,
    sc_id INT,
    PRIMARY KEY (sid, sc_id),
    FOREIGN KEY (sid) REFERENCES Student(sid),
    FOREIGN KEY (sc_id) REFERENCES Society(sc_id)
);

CREATE TABLE Course (
    cid INT PRIMARY KEY,
    cname VARCHAR(50)
);

CREATE TABLE Fac_course (
    fid INT,
    cid INT,
    PRIMARY KEY (fid, cid),
    FOREIGN KEY (fid) REFERENCES Faculty(fid),
    FOREIGN KEY (cid) REFERENCES Course(cid)
);

-- Insert sample data
INSERT INTO Dept VALUES (1, 'CSE', 500000), (2, 'IT', 400000), (3, 'AIML', 300000);
INSERT INTO Faculty VALUES (101, 'Dr. Smith', 1, 70000, 'NY', '1234567890', '1980-01-01', 12, 5),
                           (102, 'Dr. Jane', 2, 60000, 'LA', '1234509876', '1982-02-02', 8, 2),
                           (103, 'Dr. Max', 3, 55000, 'CA', '1122334455', '1985-03-03', 11, 3),
                           (104, 'Dr. Ryan', 1, 62000, 'TX', '9988776655', '1981-04-04', 15, 4),
                           (105, 'Dr. Lily', 2, 50000, 'FL', '8877665544', '1983-05-05', 7, 1);
INSERT INTO Student VALUES (1, 'Alice', 1, '9112233445', '2002-01-01', 'NY', 4),
                            (2, 'Bob', 2, NULL, '2002-02-02', 'TX', 3),
                            (3, 'Charlie', 2, '9001234567', '2001-03-03', 'CA', 2),
                            (4, 'Daisy', 3, '9111111111', '2001-04-04', 'LA', 3),
                            (5, 'Eve', 1, '9222222222', '2003-05-05', 'NY', 4);
INSERT INTO Society VALUES (201, 'Drama'), (202, 'Coding'), (203, 'Robotics');
INSERT INTO Std_soc VALUES (1, 201), (2, 202), (3, 203), (4, 201), (5, 202);
INSERT INTO Course VALUES (301, 'DBMS'), (302, 'CN'), (303, 'OS');
INSERT INTO Fac_course VALUES (101, 301), (102, 302), (103, 303);

-- Basic Queries
SELECT * FROM Faculty WHERE exp > 10 AND sal > 60000;
SELECT * FROM Student WHERE dno = 2 OR sem = 4;
UPDATE Faculty SET sal = sal + 5000 WHERE dno = 1;
UPDATE Dept SET budget = budget + 10000 WHERE dname = 'AIML';
UPDATE Student SET phone = '9333444555' WHERE sid = 4;
DELETE FROM Society WHERE sc_id = 203; -- Might fail if linked in Std_soc
DELETE FROM Student WHERE phone IS NULL;

-- Bank Database
CREATE DATABASE IF NOT EXISTS BankDB;
USE BankDB;

CREATE TABLE Branch (
    branch_id INT PRIMARY KEY,
    branch_name VARCHAR(50),
    city VARCHAR(50)
);

CREATE TABLE Customer (
    cust_id INT PRIMARY KEY,
    name VARCHAR(50),
    address VARCHAR(100),
    phone VARCHAR(15)
);

CREATE TABLE Account (
    acc_id INT PRIMARY KEY,
    cust_id INT,
    branch_id INT,
    balance DECIMAL(10,2),
    FOREIGN KEY (cust_id) REFERENCES Customer(cust_id),
    FOREIGN KEY (branch_id) REFERENCES Branch(branch_id)
);

CREATE TABLE Loan (
    loan_id INT PRIMARY KEY,
    cust_id INT,
    amount DECIMAL(10,2),
    loan_no VARCHAR(20),
    FOREIGN KEY (cust_id) REFERENCES Customer(cust_id)
);

CREATE TABLE Transaction (
    trans_id INT PRIMARY KEY,
    acc_id INT,
    amount DECIMAL(10,2),
    type VARCHAR(10),
    FOREIGN KEY (acc_id) REFERENCES Account(acc_id)
);

-- Insert records
INSERT INTO Branch VALUES (1, 'Downtown', 'NY'), (2, 'Central', 'LA');
INSERT INTO Customer VALUES (1, 'John', 'NY', '1234567890'), (2, 'Sara', 'TX', NULL), 
                            (3, 'Mike', 'CA', '1112223333');
INSERT INTO Account VALUES (101, 1, 1, 5000), (102, 2, 2, 10000), (103, 3, 1, 15000);
INSERT INTO Loan VALUES (201, 1, 20000, 'L001'), (202, 2, 15000, 'L002'), (203, 3, 10000, 'L003');
INSERT INTO Transaction VALUES (301, 101, 2000, 'Credit'), (302, 102, 3000, 'Debit');

-- Alter table & update
ALTER TABLE Loan MODIFY loan_no VARCHAR(30);
UPDATE Loan SET loan_no = 'L001-UPDATED' WHERE loan_id = 201;

-- Insert and Delete
INSERT INTO Account VALUES (104, 2, 1, 7000); -- Without phone for cust_id 2
DELETE FROM Account WHERE acc_id = 104;
```
```

---

## Learning Outcomes

By the end of this lab:

* Students will understand the implementation of fundamental SQL operations.
* Gain hands-on experience creating and manipulating database tables.
* Be able to query data using basic and conditional queries.

---

## Viva Questions & Answers

1. **Q:** What is the purpose of the `GROUP BY` clause in SQL?
   **A:** It groups rows that have the same values in specified columns and allows aggregate functions like `SUM`, `AVG`, `COUNT` to be applied to each group.

2. **Q:** What is the difference between `DELETE`, `TRUNCATE`, and `DROP`?
   **A:** `DELETE` removes specific rows based on condition, `TRUNCATE` removes all rows quickly without logging, and `DROP` removes the entire table from the database.

3. **Q:** Can a table have two primary keys?
   **A:** No, but it can have a **composite primary key** made up of more than one column.

4. **Q:** What happens if you try to delete a row referenced by a foreign key?
   **A:** It will fail unless the constraint is set to `ON DELETE CASCADE`.

5. **Q:** How is `NULL` different from `0` and empty string?
   **A:** `NULL` means unknown or no value, whereas `0` and `''` are known values (zero and empty).

---


```

---

```
