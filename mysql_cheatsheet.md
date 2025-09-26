# 📘 MySQL Cheatsheet

A quick reference guide with **explanations + examples** for common MySQL commands.

---

## 1. Database Operations
```sql
-- Create a new database
CREATE DATABASE mydb;

-- Use a database
USE mydb;

-- Show all databases
SHOW DATABASES;

-- Delete a database
DROP DATABASE mydb;
```

---

## 2. Table Operations
```sql
-- Create a new table
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    age INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Show tables
SHOW TABLES;

-- Describe table structure
DESCRIBE users;

-- Delete a table
DROP TABLE users;

-- Rename a table
RENAME TABLE users TO customers;
```

---

## 3. Insert Data
```sql
-- Insert single row
INSERT INTO users (name, email, age)
VALUES ('Rafi', 'rafi@example.com', 20);

-- Insert multiple rows
INSERT INTO users (name, email, age)
VALUES ('Saiful', 'saiful@example.com', 22),
       ('Alex', 'alex@example.com', 25);
```

---

## 4. Select Data
```sql
-- Select all
SELECT * FROM users;

-- Select specific columns
SELECT name, email FROM users;

-- With WHERE condition
SELECT * FROM users WHERE age > 20;

-- With ORDER BY
SELECT * FROM users ORDER BY age DESC;

-- With LIMIT
SELECT * FROM users LIMIT 5;

-- With DISTINCT (unique values)
SELECT DISTINCT age FROM users;
```

---

## 5. Update & Delete
```sql
-- Update
UPDATE users SET age = 30 WHERE name = 'Rafi';

-- Delete
DELETE FROM users WHERE id = 1;
```

---

## 6. Filtering Data
```sql
-- Operators
SELECT * FROM users WHERE age = 22;
SELECT * FROM users WHERE age != 22;
SELECT * FROM users WHERE age BETWEEN 18 AND 25;
SELECT * FROM users WHERE age IN (20, 22, 25);

-- Pattern matching
SELECT * FROM users WHERE name LIKE 'S%';  -- starts with S
SELECT * FROM users WHERE name LIKE '%l';  -- ends with l
SELECT * FROM users WHERE name LIKE '%ai%'; -- contains 'ai'

-- IS NULL / IS NOT NULL
SELECT * FROM users WHERE email IS NULL;
```

---

## 7. Aggregate Functions
```sql
SELECT COUNT(*) FROM users;          -- count rows
SELECT AVG(age) FROM users;          -- average
SELECT SUM(age) FROM users;          -- sum
SELECT MIN(age), MAX(age) FROM users; -- min and max
```

---

## 8. Grouping
```sql
SELECT age, COUNT(*) AS total
FROM users
GROUP BY age;

SELECT age, COUNT(*)
FROM users
GROUP BY age
HAVING COUNT(*) > 1;
```

---

## 9. Joins
```sql
-- Inner Join
SELECT users.name, orders.order_date
FROM users
INNER JOIN orders ON users.id = orders.user_id;

-- Left Join
SELECT users.name, orders.order_date
FROM users
LEFT JOIN orders ON users.id = orders.user_id;

-- Right Join
SELECT users.name, orders.order_date
FROM users
RIGHT JOIN orders ON users.id = orders.user_id;
```

---

## 10. Keys & Constraints
```sql
-- Primary Key
CREATE TABLE categories (
    id INT PRIMARY KEY,
    category_name VARCHAR(50)
);

-- Foreign Key
CREATE TABLE orders (
    id INT PRIMARY KEY,
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

-- Unique
ALTER TABLE users ADD UNIQUE (email);

-- Not Null
ALTER TABLE users MODIFY name VARCHAR(100) NOT NULL;
```

---

## 11. Indexes
```sql
-- Create index
CREATE INDEX idx_name ON users(name);

-- Drop index
DROP INDEX idx_name ON users;
```

---

## 12. Views
```sql
-- Create view
CREATE VIEW user_emails AS
SELECT name, email FROM users;

-- Select from view
SELECT * FROM user_emails;

-- Drop view
DROP VIEW user_emails;
```

---

## 13. Users & Permissions
```sql
-- Create user
CREATE USER 'rafi'@'localhost' IDENTIFIED BY 'mypassword';

-- Grant privileges
GRANT ALL PRIVILEGES ON mydb.* TO 'rafi'@'localhost';

-- Show users
SELECT user, host FROM mysql.user;

-- Drop user
DROP USER 'rafi'@'localhost';
```

---

✅ Copy this `SQL.md` file into your GitHub repo for a clean, highlighted cheatsheet!

