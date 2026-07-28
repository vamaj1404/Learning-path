# SQL Basics Notes 

## معرفی کوتاه

**SQL (Structured Query Language)** زبانی برای ارتباط با پایگاه‌های داده رابطه‌ای است.

SQL برای موارد زیر استفاده می‌شود:

* ساخت دیتابیس و جدول
* ذخیره داده‌ها
* خواندن داده‌ها
* تغییر داده‌ها
* حذف داده‌ها
* تحلیل و فیلتر کردن اطلاعات

DBMSهایی مثل:

* MySQL
* MariaDB
* Oracle Database
* PostgreSQL

برای مدیریت دیتابیس‌ها استفاده می‌شوند.

---

# Task 3 — Database Fundamentals

## مفاهیم اصلی دیتابیس

### Database چیست؟

مجموعه‌ای سازمان‌یافته از داده‌ها که برای ذخیره، مدیریت و بازیابی اطلاعات استفاده می‌شود.

ساختار معمول:

```
Database
 └── Tables
      └── Rows
           └── Columns
```

مثال:

```
Books Database

Table: books

+----+--------------+
| id | name         |
+----+--------------+
| 1  | Linux Basics |
| 2  | SQL Guide    |
+----+--------------+
```

---

# Task 4 — Database & Table Statements

## Database Commands

| دستور           | کاربرد           |
| --------------- | ---------------- |
| CREATE DATABASE | ساخت دیتابیس     |
| SHOW DATABASES  | نمایش دیتابیس‌ها |
| USE             | انتخاب دیتابیس   |
| DROP DATABASE   | حذف دیتابیس      |

---

## مثال‌ها

### ساخت دیتابیس

```sql
CREATE DATABASE thm_books;
```

---

### مشاهده دیتابیس‌ها

```sql
SHOW DATABASES;
```

---

### انتخاب دیتابیس

```sql
USE thm_books;
```

---

### حذف دیتابیس

```sql
DROP DATABASE database_name;
```

---

# Table Commands

| دستور        | کاربرد            |
| ------------ | ----------------- |
| CREATE TABLE | ساخت جدول         |
| SHOW TABLES  | نمایش جدول‌ها     |
| DESCRIBE     | نمایش ساختار جدول |
| ALTER TABLE  | تغییر جدول        |
| DROP TABLE   | حذف جدول          |

---

## ساخت جدول

```sql
CREATE TABLE books (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    published_date DATE
);
```

ساختار:

| ستون           | نوع   |
| -------------- | ----- |
| id             | عدد   |
| name           | متن   |
| published_date | تاریخ |

---

## مشاهده جدول‌ها

```sql
SHOW TABLES;
```

---

## مشاهده ساختار جدول

```sql
DESCRIBE books;
```

---

## تغییر جدول

اضافه کردن ستون:

```sql
ALTER TABLE books
ADD price INT;
```

---

# Task 5 — CRUD Operations

CRUD چهار عملیات اصلی روی داده‌ها است:

| عملیات | SQL Command | کاربرد          |
| ------ | ----------- | --------------- |
| Create | INSERT      | اضافه کردن داده |
| Read   | SELECT      | خواندن داده     |
| Update | UPDATE      | تغییر داده      |
| Delete | DELETE      | حذف داده        |

---

# CREATE (INSERT)

اضافه کردن رکورد:

```sql
INSERT INTO books
(id,name)
VALUES
(1,"SQL Basics");
```

---

# READ (SELECT)

نمایش همه اطلاعات:

```sql
SELECT * FROM books;
```

نمایش ستون خاص:

```sql
SELECT name FROM books;
```

---

# UPDATE

تغییر اطلاعات:

```sql
UPDATE books
SET name="Advanced SQL"
WHERE id=1;
```

---

# DELETE

حذف رکورد:

```sql
DELETE FROM books
WHERE id=1;
```

⚠️ بدون WHERE ممکن است کل جدول حذف شود.

---

# Task 6 — SQL Clauses

Clauseها برای کنترل Query استفاده می‌شوند.

---

# DISTINCT

حذف داده‌های تکراری:

```sql
SELECT DISTINCT name
FROM books;
```

مثال:

قبل:

```
Ethical Hacking
Ethical Hacking
```

بعد:

```
Ethical Hacking
```

---

# GROUP BY

گروه‌بندی داده‌ها:

```sql
SELECT category, COUNT(*)
FROM books
GROUP BY category;
```

خروجی:

```
Security     5
Programming  3
```

---

# ORDER BY

مرتب‌سازی:

صعودی:

```sql
ORDER BY published_date ASC;
```

نزولی:

```sql
ORDER BY published_date DESC;
```

---

# HAVING

فیلتر کردن گروه‌ها:

مثال:

```sql
SELECT category, COUNT(*)
FROM books
GROUP BY category
HAVING COUNT(*) > 2;
```

یعنی:

فقط دسته‌هایی را نشان بده که بیشتر از دو کتاب دارند.

---

# Task 7 — SQL Operators

## Logical Operators

| Operator | کاربرد                  |
| -------- | ----------------------- |
| LIKE     | جستجوی الگو             |
| AND      | همه شرط‌ها درست باشند   |
| OR       | یکی از شرط‌ها درست باشد |
| NOT      | برعکس کردن شرط          |
| BETWEEN  | محدوده                  |

---

# LIKE

جستجوی متن:

```sql
SELECT *
FROM books
WHERE name LIKE "%SQL%";
```

نتیجه:

```
SQL Basics
Advanced SQL
```

---

# AND

هر دو شرط باید برقرار باشند:

```sql
SELECT *
FROM books
WHERE category="Security"
AND id=1;
```

---

# OR

یکی از شرط‌ها کافی است:

```sql
SELECT *
FROM books
WHERE category="Security"
OR category="Programming";
```

---

# NOT

برعکس شرط:

```sql
SELECT *
FROM books
WHERE NOT category="Security";
```

---

# BETWEEN

محدوده:

```sql
SELECT *
FROM books
WHERE id BETWEEN 1 AND 5;
```

---

# Comparison Operators

| Operator | معنی          |
| -------- | ------------- |
| =        | مساوی         |
| !=       | مخالف         |
| <        | کوچک‌تر       |
| >        | بزرگ‌تر       |
| <=       | کوچک‌تر مساوی |
| >=       | بزرگ‌تر مساوی |

---

مثال:

کتاب‌های بعد از سال 2020:

```sql
SELECT *
FROM books
WHERE published_date > "2020-01-01";
```

---

# Task 8 — SQL Functions

Functions برای پردازش داده‌ها استفاده می‌شوند.

---

# String Functions

## CONCAT()

ترکیب متن‌ها:

```sql
SELECT CONCAT(name," - ",category)
FROM books;
```

خروجی:

```
SQL Basics - Security
```

---

## GROUP_CONCAT()

ترکیب چند ردیف:

```sql
SELECT category,
GROUP_CONCAT(name)
FROM books
GROUP BY category;
```

مثال:

```
Security:
Book1, Book2, Book3
```

---

## SUBSTRING()

گرفتن قسمتی از متن:

```sql
SELECT SUBSTRING(
published_date,1,4
)
FROM books;
```

خروجی:

```
2021
```

---

## LENGTH()

طول متن:

```sql
SELECT LENGTH(name)
FROM books;
```

---

# Aggregate Functions

توابع محاسباتی روی چند رکورد.

---

## COUNT()

تعداد:

```sql
SELECT COUNT(*)
FROM books;
```

---

## SUM()

جمع:

```sql
SELECT SUM(price)
FROM books;
```

---

## MAX()

بیشترین مقدار:

```sql
SELECT MAX(price)
FROM books;
```

---

## MIN()

کمترین مقدار:

```sql
SELECT MIN(price)
FROM books;
```

---

# نمونه ترکیبی (Advanced Example)

یک Query واقعی‌تر:

هدف:

> تعداد کتاب‌های هر دسته را پیدا کن، فقط دسته‌هایی که بیشتر از یک کتاب دارند، و بر اساس تعداد مرتب کن.

```sql
SELECT 
category,
COUNT(*) AS total_books

FROM books

GROUP BY category

HAVING COUNT(*) > 1

ORDER BY total_books DESC;
```

مراحل اجرا:

1. `FROM`

انتخاب جدول:

```
books
```

2. `GROUP BY`

گروه‌بندی:

```
Security
Programming
```

3. `COUNT`

تعداد کتاب‌ها:

```
Security = 5
Programming = 3
```

4. `HAVING`

فقط گروه‌های بزرگ‌تر از یک:

```
Security
Programming
```

5. `ORDER BY`

مرتب‌سازی خروجی.

---

# نمونه CRUD کامل

ایجاد جدول:

```sql
CREATE TABLE users(
id INT PRIMARY KEY AUTO_INCREMENT,
username VARCHAR(50),
email VARCHAR(100)
);
```

اضافه کردن:

```sql
INSERT INTO users(username,email)
VALUES
("ali","ali@test.com");
```

خواندن:

```sql
SELECT *
FROM users;
```

ویرایش:

```sql
UPDATE users
SET email="new@test.com"
WHERE id=1;
```

حذف:

```sql
DELETE FROM users
WHERE id=1;
```

---

# SQL Quick Reference

| کار         | دستور           |
| ----------- | --------------- |
| ساخت DB     | CREATE DATABASE |
| انتخاب DB   | USE             |
| ساخت Table  | CREATE TABLE    |
| نمایش Table | SHOW TABLES     |
| ساخت داده   | INSERT          |
| خواندن      | SELECT          |
| تغییر       | UPDATE          |
| حذف         | DELETE          |
| فیلتر       | WHERE           |
| گروه‌بندی   | GROUP BY        |
| مرتب‌سازی   | ORDER BY        |
| شرط گروه    | HAVING          |
| حذف تکرار   | DISTINCT        |
| شمارش       | COUNT           |
| جمع         | SUM             |
| بیشترین     | MAX             |
| کمترین      | MIN             |

---

این فایل برای GitHub به‌عنوان **SQL Beginner Cheat Sheet + TryHackMe Tasks 3-8 Notes** مناسب است.
