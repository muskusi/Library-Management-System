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

