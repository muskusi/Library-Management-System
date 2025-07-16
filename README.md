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
📋 CTAS Operations
🔹 Task 6: Book Issue Summary
```sql
CREATE TABLE book_issued_cnt AS
SELECT b.isbn, b.book_title, COUNT(ist.issued_id) AS issue_count
FROM issued_status ist
JOIN books b ON ist.issued_book_isbn = b.isbn
GROUP BY b.isbn, b.book_title;
```
📈 Data Analysis & Insights
🔹 Task 7: Books in Classic Category
```sql
SELECT * FROM books WHERE category = 'Classic';
```
🔹 Task 8: Total Rental Income by Category
```sql
SELECT b.category, SUM(b.rental_price), COUNT(*)
FROM issued_status ist
JOIN books b ON b.isbn = ist.issued_book_isbn
GROUP BY 1;
```
🔹 Task 9: Recent Registrations (180 Days)
```sql
SELECT * FROM members
WHERE reg_date >= CURRENT_DATE - INTERVAL '180 days';
```
🔹 Task 10: Employees with Their Manager and Branch
```sql
SELECT e1.emp_id, e1.emp_name, e1.position, e1.salary, b.*, e2.emp_name AS manager
FROM employees e1
JOIN branch b ON e1.branch_id = b.branch_id
JOIN employees e2 ON e2.emp_id = b.manager_id;
```
💼 Advanced SQL Queries
🔹 Task 11: Expensive Books Table
```sql
CREATE TABLE expensive_books AS
SELECT * FROM books
WHERE rental_price > 7.00;
```
🔹 Task 12: Books Not Yet Returned
```sql
SELECT * FROM issued_status ist
LEFT JOIN return_status rs ON rs.issued_id = ist.issued_id
WHERE rs.return_id IS NULL;
```
🔹 Task 13: Overdue Books (>30 Days)
```sql
SELECT ist.issued_member_id, m.member_name, bk.book_title, ist.issued_date, 
       CURRENT_DATE - ist.issued_date AS over_dues_days
FROM issued_status ist
JOIN members m ON m.member_id = ist.issued_member_id
JOIN books bk ON bk.isbn = ist.issued_book_isbn
LEFT JOIN return_status rs ON rs.issued_id = ist.issued_id
WHERE rs.return_date IS NULL AND (CURRENT_DATE - ist.issued_date) > 30;
```
🔹 Task 17: Top 3 Employees by Issued Books
```sql
SELECT e.emp_name, b.*, COUNT(ist.issued_id) AS no_book_issued
FROM issued_status ist
JOIN employees e ON e.emp_id = ist.issued_emp_id
JOIN branch b ON e.branch_id = b.branch_id
GROUP BY e.emp_name, b.branch_id
ORDER BY no_book_issued DESC
LIMIT 3;
```
🧠 Stored Procedure: Issue a Book
```sql
CREATE OR REPLACE PROCEDURE issue_book(p_issued_id VARCHAR(10), p_issued_member_id VARCHAR(30), p_issued_book_isbn VARCHAR(30), p_issued_emp_id VARCHAR(10))
LANGUAGE plpgsql AS $$
DECLARE v_status VARCHAR(10);
BEGIN
    SELECT status INTO v_status FROM books WHERE isbn = p_issued_book_isbn;
    
    IF v_status = 'yes' THEN
        INSERT INTO issued_status(issued_id, issued_member_id, issued_date, issued_book_isbn, issued_emp_id)
        VALUES (p_issued_id, p_issued_member_id, CURRENT_DATE, p_issued_book_isbn, p_issued_emp_id);

        UPDATE books SET status = 'no' WHERE isbn = p_issued_book_isbn;

        RAISE NOTICE 'Book records added successfully for book isbn: %', p_issued_book_isbn;
    ELSE
        RAISE NOTICE 'Book is currently not available: %', p_issued_book_isbn;
    END IF;
END;
$$;
```
## 📊 Reports & Outputs
Database schema with primary and foreign keys

Summary of active members and top employees

Branch revenue analysis

Overdue books and return tracking

## 👤 Author

**Samskruthi Musku**  
Data Analyst  
🔗 [LinkedIn](https://www.linkedin.com/in/samskruthi-musku/)  
📎 [Portfolio](https://samskruthireddy088.wixsite.com/my-site-2)


