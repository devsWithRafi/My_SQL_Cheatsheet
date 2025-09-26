# MySQL Cheat Sheet

A beginner-friendly MySQL reference with **explanations** and **examples**.  
Use this as a quick guide while working with SQL queries.

---

## 📂 Database Management

### Create Database
```sql
CREATE DATABASE SchoolDB;
```
✅ Creates a new database.

### Drop Database
```sql
DROP DATABASE SchoolDB;
```
⚠️ Deletes the entire database permanently.

### Use Database
```sql
USE SchoolDB;
```
👉 Selects the database to work on.

---

## 📑 Table Operations

### Create Table
```sql
CREATE TABLE Students (
   StudentID INT AUTO_INCREMENT PRIMARY KEY,
   FirstName VARCHAR(50) NOT NULL,
   LastName VARCHAR(50) NOT NULL,
   Age INT,
   Department VARCHAR(50)
);
```
✅ Creates a table with columns.

### Drop Table
```sql
DROP TABLE Students;
```
⚠️ Removes the whole table.

### Alter Table
```sql
ALTER TABLE Students ADD Email VARCHAR(100);
ALTER TABLE Students DROP COLUMN Email;
```
👉 Used to **add/remove/modify** columns.

---

## 🔒 Constraints

- **NOT NULL** → Ensures column cannot be empty.  
- **UNIQUE** → Ensures all values are unique.  
- **PRIMARY KEY** → Unique + Not Null (row identifier).  
- **FOREIGN KEY** → Links rows between two tables.  
- **CHECK** → Enforces a condition.  
- **DEFAULT** → Sets a default value.  
- **INDEX** → Improves search performance.  

**Examples:**

```sql
ALTER TABLE Students ADD CONSTRAINT UC_Email UNIQUE (Email);
ALTER TABLE Students ADD CONSTRAINT CHK_Age CHECK (Age >= 16);
ALTER TABLE Students ADD CONSTRAINT DF_Department DEFAULT 'General' FOR Department;
```

---

## ✍️ Data Handling

### Insert Data
```sql
INSERT INTO Students (FirstName, LastName, Age, Department)
VALUES ('Alice', 'Brown', 20, 'Computer Science');
```

### Select Data
```sql
SELECT * FROM Students;
```

### Select Distinct
```sql
SELECT DISTINCT Department FROM Students;
```

### Where Clause
```sql
SELECT * FROM Students WHERE Age > 20;
```

### Order By
```sql
SELECT * FROM Students ORDER BY Age DESC;
```

### Update
```sql
UPDATE Students SET Age = 21 WHERE FirstName = 'Alice';
```

### Delete
```sql
DELETE FROM Students WHERE LastName = 'Smith';
```

---

## 🔢 Aggregate Functions

```sql
SELECT MIN(Age) AS Youngest, MAX(Age) AS Oldest FROM Students;
SELECT COUNT(*) FROM Students;
SELECT SUM(Age) FROM Students;
SELECT AVG(Age) FROM Students;
```

---

## 🔍 Pattern Matching

```sql
SELECT * FROM Students WHERE FirstName LIKE 'A%';   -- starts with A
SELECT * FROM Students WHERE LastName LIKE '_ohn'; -- second char match
```

---

## 🎯 Filtering

```sql
SELECT * FROM Students WHERE Department IN ('Math', 'Physics');
SELECT * FROM Students WHERE Age BETWEEN 18 AND 22;
```

---

## 🏷️ Aliases

```sql
SELECT FirstName AS Name, Department AS Dept FROM Students;
```

---

## 🔗 Joins

```sql
-- Inner Join
SELECT s.FirstName, c.CourseName
FROM Students s
INNER JOIN Enrollments e ON s.StudentID = e.StudentID
INNER JOIN Courses c ON e.CourseID = c.CourseID;

-- Left Join
SELECT s.FirstName, c.CourseName
FROM Students s
LEFT JOIN Enrollments e ON s.StudentID = e.StudentID
LEFT JOIN Courses c ON e.CourseID = c.CourseID;
```

---

## 📊 Grouping

```sql
SELECT Department, COUNT(*) FROM Students GROUP BY Department;
SELECT Department, COUNT(*) FROM Students GROUP BY Department HAVING COUNT(*) > 2;
```

---

## 🌀 Subqueries

```sql
SELECT * FROM Students s
WHERE EXISTS (SELECT * FROM Enrollments e WHERE e.StudentID = s.StudentID);

SELECT * FROM Students
WHERE Age > ALL (SELECT Age FROM Students WHERE Department = 'Physics');
```

---

## ⚡ Logic

```sql
SELECT FirstName,
CASE
   WHEN Age < 20 THEN 'Teen'
   WHEN Age BETWEEN 20 AND 22 THEN 'Young Adult'
   ELSE 'Adult'
END AS AgeGroup
FROM Students;
```

---

## 🛠 Handling Nulls

```sql
SELECT IFNULL(Email, 'No Email Provided') FROM Students;
```

---

## 📅 Dates

```sql
SELECT * FROM Students WHERE BirthDate > '2000-01-01';
```

---

## 👀 Views

```sql
CREATE VIEW StudentDetails AS
SELECT FirstName, LastName, Department FROM Students;
```

---

## 🔐 Security

❌ **Bad (SQL Injection):**
```sql
SELECT * FROM Users WHERE Name = '" + userInput + "';
```

✅ **Safe (Prepared Statements):**
```sql
SELECT * FROM Users WHERE Name = ?;
```

---

## 💡 Comments

```sql
-- Single line comment

/* Multi
   line
   comment */
```

---

🚀 This cheat sheet is designed for **MySQL beginners** but also covers advanced features.
