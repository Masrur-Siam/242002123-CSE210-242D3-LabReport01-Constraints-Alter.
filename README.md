# Library Lab Database

![MySQL](https://img.shields.io/badge/Database-MySQL-blue) ![Language](https://img.shields.io/badge/Language-SQL-orange)

## Table of Contents

* [Overview](#overview)
* [Database Structure](#database-structure)
* [Features](#features)
* [Usage](#usage)
* [Example Queries](#example-queries)
* [Notes](#notes)

---

## Overview

This project demonstrates a **Library Management Database** using MySQL. It includes tables for **members**, **books**, and **borrowing records**, with proper constraints like **Primary Key, Foreign Key, Unique, and Check**.
It also demonstrates **data insertion, constraint testing**, and **ALTER TABLE modifications**.

---

## Database Structure

### MEMBER

| Column   | Type         | Constraints             |
| -------- | ------------ | ----------------------- |
| MemberID | INT          | PRIMARY KEY             |
| FullName | VARCHAR(100) | NOT NULL                |
| Email    | VARCHAR(100) | NOT NULL, UNIQUE        |
| Age      | INT          | CHECK (Age >= 12)       |
| Phone    | VARCHAR(15)  | NOT NULL, DEFAULT 'N/A' |

### BOOK

| Column       | Type         | Constraints         |
| ------------ | ------------ | ------------------- |
| BookID       | INT          | PRIMARY KEY         |
| Title        | VARCHAR(150) | NOT NULL            |
| ISBN         | VARCHAR(50)  | NOT NULL, UNIQUE    |
| Price        | DECIMAL(8,2) | CHECK (Price >= 0)  |
| Availability | ENUM         | DEFAULT 'AVAILABLE' |

### BORROW (formerly LOAN)

| Column   | Type | Constraints                    |
| -------- | ---- | ------------------------------ |
| LoanID   | INT  | PRIMARY KEY                    |
| MemberID | INT  | FOREIGN KEY → MEMBER(MemberID) |
| BookID   | INT  | FOREIGN KEY → BOOK(BookID)     |

---

## Features

* Table creation with **constraints**: PK, FK, UNIQUE, CHECK
* Inserting **sample data** for members, books, and borrow records
* Demonstrates **constraint violation errors**:

  * Duplicate Email
  * Negative Book Price
  * Borrow record with missing MemberID
* **ALTER TABLE operations**:

  * Add/drop columns
  * Modify column data types
  * Rename table/columns
  * Add named CHECK constraints

---

## Usage

1. Install **XAMPP** and start **Apache** & **MySQL**.
2. Open **phpMyAdmin**.
3. Run the SQL file `library_lab.sql` to create database, tables, and insert sample data.
4. Explore the database and test constraints.

---

## Example Queries

```sql
-- Insert a new member
INSERT INTO MEMBER (MemberID, FullName, Email, Age, Phone)
VALUES (6, 'Test User', 'test@gmail.com', 21, 'N/A');

-- Insert a new book
INSERT INTO BOOK (BookID, Title, ISBN, Price, Availability)
VALUES (6, 'Advanced SQL', 'ISBN006', 550.00, 'AVAILABLE');

-- Record a borrow transaction
INSERT INTO BORROW (LoanID, MemberID, BookID)
VALUES (7, 6, 6);

-- Select all members
SELECT * FROM MEMBER;

-- Select all available books
SELECT * FROM BOOK WHERE Availability='AVAILABLE';

-- Check borrow records
SELECT * FROM BORROW;
```

---

## Notes

* Designed for **learning and lab practice**.
* Constraint violations are intentional to demonstrate MySQL error handling.
* Works best in **XAMPP with MySQL 5.7+**.
* Can be extended with features like **book categories, member subscriptions**, or **late fees**.

---

