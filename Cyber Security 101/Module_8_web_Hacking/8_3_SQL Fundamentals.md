
```markdown
# SQL Basics Cheat Sheet (Tasks 3-8)

A practical SQL reference covering database fundamentals, CRUD operations, clauses, operators, and functions.

Based on TryHackMe SQL learning tasks.

---

# Table of Contents

- [Introduction](#introduction)
- [Database Fundamentals](#database-fundamentals)
- [Database & Table Commands](#database--table-commands)
- [CRUD Operations](#crud-operations)
- [SQL Clauses](#sql-clauses)
- [SQL Operators](#sql-operators)
- [SQL Functions](#sql-functions)
- [Advanced Examples](#advanced-examples)
- [Quick Reference](#quick-reference)

---

# Introduction

## What is SQL?

SQL (**Structured Query Language**) is a language used to communicate with relational databases.

SQL allows users to:

- Create databases and tables
- Insert and retrieve data
- Update existing information
- Delete records
- Analyze and manipulate data


Common Database Management Systems (DBMS):

- MySQL
- MariaDB
- PostgreSQL
- Oracle Database


Basic structure:

```

Database
└── Tables
└── Rows
└── Columns

```

Example:

```

Books Database

+----+----------------+
| id | name           |
+----+----------------+
| 1  | Linux Basics   |
| 2  | SQL Guide      |
+----+----------------+

````

---

# Database Fundamentals

## Database Commands

| Command | Description |
|---------|-------------|
| CREATE DATABASE | Create a new database |
| SHOW DATABASES | List databases |
| USE | Select a database |
| DROP DATABASE | Delete a database |


## Examples

Create database:

```sql
CREATE DATABASE thm_books;
````

Show databases:

```sql
SHOW DATABASES;
```

Select database:

```sql
USE thm_books;
```

Delete database:

```sql
DROP DATABASE database_name;
```

---

# Database & Table Commands

## Table Commands

| Command      | Description          |
| ------------ | -------------------- |
| CREATE TABLE | Create a table       |
| SHOW TABLES  | List tables          |
| DESCRIBE     | Show table structure |
| ALTER TABLE  | Modify table         |
| DROP TABLE   | Delete table         |

## Create Table

```sql
CREATE TABLE books (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    published_date DATE
);
```

## View Tables

```sql
SHOW TABLES;
```

## View Table Structure

```sql
DESCRIBE books;
```

## Modify Table

Add a new column:

```sql
ALTER TABLE books
ADD price INT;
```

---

# CRUD Operations

CRUD represents the four basic database operations:

| Operation | SQL Command | Purpose       |
| --------- | ----------- | ------------- |
| Create    | INSERT      | Add new data  |
| Read      | SELECT      | Retrieve data |
| Update    | UPDATE      | Modify data   |
| Delete    | DELETE      | Remove data   |

---

# CREATE (INSERT)

Insert new records:

```sql
INSERT INTO books
(id,name)
VALUES
(1,'SQL Basics');
```

---

# READ (SELECT)

Select everything:

```sql
SELECT * FROM books;
```

Select specific columns:

```sql
SELECT name FROM books;
```

---

# UPDATE

Modify existing data:

```sql
UPDATE books
SET name='Advanced SQL'
WHERE id=1;
```

---

# DELETE

Remove records:

```sql
DELETE FROM books
WHERE id=1;
```

⚠️ Always use `WHERE` to avoid deleting all rows.

---

# SQL Clauses

Clauses control how SQL queries process and return data.

---

## DISTINCT

Remove duplicate values.

Example:

```sql
SELECT DISTINCT name
FROM books;
```

Before:

```
Ethical Hacking
Ethical Hacking
```

After:

```
Ethical Hacking
```

---

## GROUP BY

Group records based on a column.

Example:

```sql
SELECT category, COUNT(*)
FROM books
GROUP BY category;
```

Output:

```
Security       5
Programming    3
```

---

## ORDER BY

Sort query results.

Ascending:

```sql
ORDER BY published_date ASC;
```

Descending:

```sql
ORDER BY published_date DESC;
```

---

## HAVING

Filter grouped results.

Example:

```sql
SELECT category, COUNT(*)
FROM books
GROUP BY category
HAVING COUNT(*) > 2;
```

Meaning:

Return only categories containing more than two books.

---

# SQL Operators

Operators help filter and compare data.

---

## Logical Operators

| Operator | Description                    |
| -------- | ------------------------------ |
| LIKE     | Search patterns                |
| AND      | All conditions must be true    |
| OR       | At least one condition is true |
| NOT      | Reverse a condition            |
| BETWEEN  | Check a range                  |

---

## LIKE

Search inside text:

```sql
SELECT *
FROM books
WHERE name LIKE '%SQL%';
```

---

## AND

Both conditions must match:

```sql
SELECT *
FROM books
WHERE category='Security'
AND id=1;
```

---

## OR

One condition must match:

```sql
SELECT *
FROM books
WHERE category='Security'
OR category='Programming';
```

---

## NOT

Exclude results:

```sql
SELECT *
FROM books
WHERE NOT category='Security';
```

---

## BETWEEN

Check values inside a range:

```sql
SELECT *
FROM books
WHERE id BETWEEN 1 AND 5;
```

---

# Comparison Operators

| Operator | Meaning               |
| -------- | --------------------- |
| =        | Equal                 |
| !=       | Not Equal             |
| <        | Less Than             |
| >        | Greater Than          |
| <=       | Less Than or Equal    |
| >=       | Greater Than or Equal |

Example:

Books published after 2020:

```sql
SELECT *
FROM books
WHERE published_date > '2020-01-01';
```

---

# SQL Functions

Functions process and manipulate data.

---

# String Functions

## CONCAT()

Combine strings:

```sql
SELECT CONCAT(name,' - ',category)
FROM books;
```

Example output:

```
SQL Basics - Security
```

---

## GROUP_CONCAT()

Combine multiple rows:

```sql
SELECT category,
GROUP_CONCAT(name)
FROM books
GROUP BY category;
```

Example:

```
Security:
Book1, Book2, Book3
```

---

## SUBSTRING()

Extract part of a string:

```sql
SELECT SUBSTRING(published_date,1,4)
FROM books;
```

Output:

```
2021
```

---

## LENGTH()

Count characters:

```sql
SELECT LENGTH(name)
FROM books;
```

---

# Aggregate Functions

## COUNT()

Count rows:

```sql
SELECT COUNT(*)
FROM books;
```

## SUM()

Calculate total:

```sql
SELECT SUM(price)
FROM books;
```

## MAX()

Find highest value:

```sql
SELECT MAX(price)
FROM books;
```

## MIN()

Find lowest value:

```sql
SELECT MIN(price)
FROM books;
```

---

# Advanced Examples

## Count Books Per Category

Goal:

Find categories with more than one book and sort them.

```sql
SELECT 
    category,
    COUNT(*) AS total_books

FROM books

GROUP BY category

HAVING COUNT(*) > 1

ORDER BY total_books DESC;
```

Execution flow:

```
FROM
 ↓
GROUP BY
 ↓
COUNT()
 ↓
HAVING
 ↓
ORDER BY
```

---

# Complete CRUD Example

## Create Table

```sql
CREATE TABLE users(
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50),
    email VARCHAR(100)
);
```

## Insert Data

```sql
INSERT INTO users(username,email)
VALUES
('alice','alice@test.com');
```

## Read Data

```sql
SELECT *
FROM users;
```

## Update Data

```sql
UPDATE users
SET email='new@test.com'
WHERE id=1;
```

## Delete Data

```sql
DELETE FROM users
WHERE id=1;
```

---

# Quick Reference

| Task              | SQL Command     |
| ----------------- | --------------- |
| Create Database   | CREATE DATABASE |
| Select Database   | USE             |
| Create Table      | CREATE TABLE    |
| Show Tables       | SHOW TABLES     |
| Insert Data       | INSERT          |
| Read Data         | SELECT          |
| Update Data       | UPDATE          |
| Delete Data       | DELETE          |
| Filter Data       | WHERE           |
| Group Data        | GROUP BY        |
| Sort Data         | ORDER BY        |
| Filter Groups     | HAVING          |
| Remove Duplicates | DISTINCT        |
| Count Records     | COUNT           |
| Sum Values        | SUM             |
| Highest Value     | MAX             |
| Lowest Value      | MIN             |

---
