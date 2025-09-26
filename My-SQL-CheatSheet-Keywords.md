# MySQL Cheat Sheet

A beginner-friendly MySQL reference with **explanations**, **examples**, and **keyword notes**.  
Use this as a quick guide while working with SQL queries.

---

## 📂 Database Management

### Create Database
```sql
CREATE DATABASE SchoolDB;
```
**Keyword Notes:**
- `CREATE` → Used to create new databases or tables.  
- `DATABASE` → Specifies that you are creating a database.  

### Drop Database
```sql
DROP DATABASE SchoolDB;
```
**Keyword Notes:**
- `DROP` → Deletes an object (database, table, column, etc.).  
- `DATABASE` → Specifies you are deleting a database.  

### Use Database
```sql
USE SchoolDB;
```
**Keyword Notes:**
- `USE` → Tells SQL which database to work in.  

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
**Keyword Notes:**
- `CREATE TABLE` → Makes a new table.  
- `AUTO_INCREMENT` → Automatically generates sequential numbers.  
- `PRIMARY KEY` → Unique identifier for each row.  
- `NOT NULL` → Column cannot have empty values.  

### Drop Table
```sql
DROP TABLE Students;
```
**Keyword Notes:**
- `DROP TABLE` → Deletes the entire table and its data.  

### Alter Table
```sql
ALTER TABLE Students ADD Email VARCHAR(100);
ALTER TABLE Students DROP COLUMN Email;
```
**Keyword Notes:**
- `ALTER TABLE` → Used to modify an existing table.  
- `ADD` → Adds a new column or constraint.  
- `DROP COLUMN` → Removes a column from the table.  

---

## 🔒 Constraints

**Examples:**
```sql
ALTER TABLE Students ADD CONSTRAINT UC_Email UNIQUE (Email);
ALTER TABLE Students ADD CONSTRAINT CHK_Age CHECK (Age >= 16);
ALTER TABLE Students ADD CONSTRAINT DF_Department DEFAULT 'General' FOR Department;
```
**Keyword Notes:**
- `CONSTRAINT` → Defines a rule on the table.  
- `UNIQUE` → Ensures all values are different.  
- `CHECK` → Ensures a condition is true for values.  
- `DEFAULT` → Assigns a default value when none is provided.  

---

## ✍️ Data Handling

### Insert Data
```sql
INSERT INTO Students (FirstName, LastName, Age, Department)
VALUES ('Alice', 'Brown', 20, 'Computer Science');
```
**Keyword Notes:**
- `INSERT INTO` → Adds new data into a table.  
- `VALUES` → The actual data being inserted.  

### Select Data
```sql
SELECT * FROM Students;
```
**Keyword Notes:**
- `SELECT` → Retrieves data from the table.  
- `*` → Means all columns.  
- `FROM` → Specifies the source table.  

### Select Distinct
```sql
SELECT DISTINCT Department FROM Students;
```
**Keyword Notes:**
- `DISTINCT` → Removes duplicate values.  

### Where Clause
```sql
SELECT * FROM Students WHERE Age > 20;
```
**Keyword Notes:**
- `WHERE` → Filters rows based on a condition.  
- `>` → Comparison operator (greater than).  

### Order By
```sql
SELECT * FROM Students ORDER BY Age DESC;
```
**Keyword Notes:**
- `ORDER BY` → Sorts the results.  
- `DESC` → Descending order (high → low).  
- `ASC` → Ascending order (low → high).  

### Update
```sql
UPDATE Students SET Age = 21 WHERE FirstName = 'Alice';
```
**Keyword Notes:**
- `UPDATE` → Modifies existing rows.  
- `SET` → Defines new values.  
- `WHERE` → Filters which rows to update.  

### Delete
```sql
DELETE FROM Students WHERE LastName = 'Smith';
```
**Keyword Notes:**
- `DELETE` → Removes rows.  
- `WHERE` → Prevents deleting everything by mistake.  

---

## 🔢 Aggregate Functions

```sql
SELECT MIN(Age) AS Youngest, MAX(Age) AS Oldest FROM Students;
SELECT COUNT(*) FROM Students;
SELECT SUM(Age) FROM Students;
SELECT AVG(Age) FROM Students;
```
**Keyword Notes:**
- `MIN` → Finds smallest value.  
- `MAX` → Finds largest value.  
- `COUNT` → Counts number of rows.  
- `SUM` → Adds up values.  
- `AVG` → Finds average.  
- `AS` → Renames output column.  

---

## 🔍 Pattern Matching

```sql
SELECT * FROM Students WHERE FirstName LIKE 'A%';   -- starts with A
SELECT * FROM Students WHERE LastName LIKE '_ohn'; -- second char match
```
**Keyword Notes:**
- `LIKE` → Used for pattern matching.  
- `%` → Matches any sequence of characters.  
- `_` → Matches exactly one character.  

---

## 🎯 Filtering

```sql
SELECT * FROM Students WHERE Department IN ('Math', 'Physics');
SELECT * FROM Students WHERE Age BETWEEN 18 AND 22;
```
**Keyword Notes:**
- `IN` → Matches against multiple values.  
- `BETWEEN` → Checks if value is within a range.  

---

## 🏷️ Aliases

```sql
SELECT FirstName AS Name, Department AS Dept FROM Students;
```
**Keyword Notes:**
- `AS` → Creates a temporary name (alias) for columns or tables.  

---

## 🔗 Joins

```sql
-- Inner Join
SELECT s.FirstName, c.CourseName
FROM Students s
INNER JOIN Enrollments e ON s.StudentID = e.StudentID
INNER JOIN Courses c ON e.CourseID = c.CourseID;
```
**Keyword Notes:**
- `INNER JOIN` → Returns only matching rows from both tables.  
- `ON` → Condition to match rows.  

```sql
-- Left Join
SELECT s.FirstName, c.CourseName
FROM Students s
LEFT JOIN Enrollments e ON s.StudentID = e.StudentID
LEFT JOIN Courses c ON e.CourseID = c.CourseID;
```
**Keyword Notes:**
- `LEFT JOIN` → Returns all rows from left table + matching rows from right table.  

---

## 📊 Grouping

```sql
SELECT Department, COUNT(*) FROM Students GROUP BY Department;
SELECT Department, COUNT(*) FROM Students GROUP BY Department HAVING COUNT(*) > 2;
```
**Keyword Notes:**
- `GROUP BY` → Groups rows with same values.  
- `HAVING` → Filters groups (like WHERE but for groups).  

---

## 🌀 Subqueries

```sql
SELECT * FROM Students s
WHERE EXISTS (SELECT * FROM Enrollments e WHERE e.StudentID = s.StudentID);
```
**Keyword Notes:**
- `EXISTS` → Checks if subquery returns results.  

```sql
SELECT * FROM Students
WHERE Age > ALL (SELECT Age FROM Students WHERE Department = 'Physics');
```
**Keyword Notes:**
- `ALL` → Condition must be true for all values.  
- `ANY` → Condition must be true for at least one value.  

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
**Keyword Notes:**
- `CASE` → Conditional logic in SQL.  
- `WHEN` → Condition to check.  
- `THEN` → Result if condition is true.  
- `ELSE` → Result if no condition is met.  

---

## 🛠 Handling Nulls

```sql
SELECT IFNULL(Email, 'No Email Provided') FROM Students;
```
**Keyword Notes:**
- `IFNULL` → Replaces NULL values with a default.  

---

## 📅 Dates

```sql
SELECT * FROM Students WHERE BirthDate > '2000-01-01';
```
**Keyword Notes:**
- `>` → Comparison operator.  
- `DATE` → MySQL data type for storing dates.  

---

## 👀 Views

```sql
CREATE VIEW StudentDetails AS
SELECT FirstName, LastName, Department FROM Students;
```
**Keyword Notes:**
- `VIEW` → A saved query that behaves like a virtual table.  

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
**Keyword Notes:**
- `?` → Placeholder for safe user input in prepared statements.  

---

## 💡 Comments

```sql
-- Single line comment

/* Multi
   line
   comment */
```
**Keyword Notes:**
- `--` → Single line comment.  
- `/* ... */` → Multi-line comment.  

---

🚀 This cheat sheet is designed for **MySQL beginners** but also covers advanced features, with keyword explanations for quick learning.
