# 📚 Library Management System using SQL

## 📝 Project Overview

**Project Title**: Library Management System  
**Database**: `library_db`  
**Objective**: To design and implement a full-featured Library Management System using SQL that demonstrates skills in database creation, normalization, querying, and reporting.

![Library_project](https://github.com/najirh/Library-System-Management---P2/blob/main/library.jpg)

---

## 🎯 Objectives

- Design and create a normalized relational database for a library system.
- Perform **CRUD** operations to manage library records.
- Use **CTAS** (Create Table As Select) for reporting.
- Write **advanced SQL queries** for analysis and insights.

---

## 🏗️ Database Schema

![ERD](https://github.com/najirh/Library-System-Management---P2/blob/main/library_erd.png)

Tables:

- `branch`
- `employees`
- `members`
- `books`
- `issued_status`
- `return_status`

---

## 🔧 Table Creation

```sql
-- Sample: Create Branch Table
CREATE TABLE branch (
  branch_id VARCHAR(10) PRIMARY KEY,
  manager_id VARCHAR(10),
  branch_address VARCHAR(30),
  contact_no VARCHAR(15)
);
-- Full table creation scripts in source code above
```
📊 CRUD Operations
🔹 Task 1: Add a New Book
```sql
INSERT INTO books(isbn, book_title, category, rental_price, status, author, publisher)
VALUES('978-1-60129-456-2', 'To Kill a Mockingbird', 'Classic', 6.00, 'yes', 'Harper Lee', 'J.B. Lippincott & Co.');
```
🔹 Task 2: Update Member Address
```sql
UPDATE members
SET member_address = '125 Oak St'
WHERE member_id = 'C103';
```
🔹 Task 3: Delete Issued Record
```sql
DELETE FROM issued_status
WHERE issued_id = 'IS121';
```
🔹 Task 4: Books Issued by Specific Employee
```sql
SELECT * FROM issued_status
WHERE issued_emp_id = 'E101';
```

🔹 Task 5: Members Issuing More Than One Book
```sql
SELECT issued_emp_id, COUNT(*)
FROM issued_status
GROUP BY 1
HAVING COUNT(*) > 1;
```
