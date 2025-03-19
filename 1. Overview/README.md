# Week 1: Overview

## Table of Contents
<ol>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#objectives">Objectives</a></li>
    <li><a href="#sql-basics">SQL Basics</a></li>
    <li><a href="#normalization">Normalization</a></li>
</ol>

## Overview
This document provides basic knowledge about Databases (DB) and SQL (Structured Query Language), covering definitions, roles, and core concepts. It helps learners get familiar with organizing and managing data, using database management systems, and writing basic SQL queries.

## Objectives
- Understand the basic concept of databases.
- Understand the concept and role of relational databases.
- Understand SQL and its usage.
- Identify data types in SQL.
- Recognize the importance of primary and foreign keys.
- Prepare practice tools.

## SQL Basics
- **SQL definition:**
    - A standard language used in relational database systems (RDBMS).
    - Easy to learn and widely applied.
    - Each RDBMS uses its own version of SQL.
- **SQL statement types:**
    - **DDL (Data Definition Language):**
        - `CREATE`: Create a table, view, or other objects in the database.
        - `ALTER`: Modify an existing object.
        - `DROP`: Remove a table, view, or other objects in the database.
    - **DML (Data Manipulation Language):**
        - `INSERT`: Add new records.
        - `UPDATE`: Modify records.
        - `DELETE`: Remove records.
    - **DQL (Data Query Language):**
        - `SELECT`: Retrieve records from one or more tables.
    - **DCL (Data Control Language):**
        - `GRANT`: Assign a privilege to a user.
        - `REVOKE`: Revoke a previously assigned privilege.
    - **TCL (Transaction Control Language):**
        - `COMMIT`: Save changes.
        - `ROLLBACK`: Revert to the state before the changes.
        - `SAVEPOINT`: Set points within a transaction to rollback to.
        - `SET TRANSACTION`: Name a transaction.
- **SQL data types:**
    - Character:
        - `CHAR`: Fixed-length character string | Size: Up to 2000 bytes.
        - `VARCHAR2`: Variable-length character string | Size: Up to 4000 bytes.
    - Numeric:
        - `NUMBER[(p[, s])]`: Numeric type with up to p digits including decimals | Max size: 38 digits.
        - `FLOAT`: Real number type, with up to p binary digits | Max size: 38 decimal digits.
    - Date & Time:
        - `DATE`: Date and time type.
        - `TIMESTAMP`: Date type with millisecond support.
- **SQL operators:**
    - Arithmetic: `+`, `-`, `*`, `/`, `%`.
    - Comparison: `=`, `<>`, `>`, `<`, `>=`, `<=`.
    - Logical: `AND`, `OR`, `LIKE`, `BETWEEN`.


## Normalization
- **Definition:** Normalization is the process of organizing data in a database to reduce redundancy and improve data integrity. It involves dividing a database into smaller, related tables and defining relationships between them to enhance efficiency and consistency.
- **Benefits:**
    - Minimizes data duplication, ensuring consistency across the database.
    - Simplifies maintenance by eliminating redundancy.
    - Improves data integrity by enforcing constraints and relationships.
    - Optimizes database performance for queries and updates.
  
1. `1NF`(First Normal Form): Ensures that each column contains atomic values, and each record (row) is unique. No repeating groups or arrays within a column are allowed.
      - **Initial Table (Not in 1NF)**:

        | Student_ID | Name        | Subjects       | Contact          |  
        |------------|-------------|----------------|------------------|  
        | 1          | John Doe    | Math, Science  | 123-456-7890     |  
        | 2          | Jane Smith  | Science, Art   | 987-654-3210     |

          - **Issues:**:
              - The `Subjects` column contains multiple values (not atomic).
              - This violates the rule that each column should contain atomic values (indivisible data)
          - **Transformed Table (In 1NF):**

            | Student_ID | Name        | Subject     | Contact          |  
            |------------|-------------|-------------|------------------|  
            | 1          | John Doe    | Math        | 123-456-7890     |  
            | 1          | John Doe    | Science     | 123-456-7890     |  
            | 2          | Jane Smith  | Science     | 987-654-3210     |  
            | 2          | Jane Smith  | Art         | 987-654-3210     |

2. `2NF` (Second Normal Form): Builds on 1NF by ensuring all non-key attributes are fully dependent on the primary key. It removes partial dependencies on composite primary keys.
      - **Initial Table (Not in 2NF)**:

        | Student_ID | Course_ID | Student_Name | Course_Name     | Instructor      |  
        |------------|-----------|--------------|-----------------|-----------------|  
        | 1          | C1        | John Doe     | Mathematics     | Dr. Smith       |  
        | 1          | C2        | John Doe     | Physics         | Dr. Brown       |  
        | 2          | C1        | Jane Smith   | Mathematics     | Dr. Smith       |      

      - **Issues**:
          - The primary key is a composite key (`Student_ID`, `Course_ID`).
          - Non-key attributes like `Student_Name` and `Course_Name` depend only on part of the composite key, violating 2NF rules (partial dependency).

      - **Transformed Table (In 2NF):**

        **Table 1: Students**

        | Student_ID | Student_Name |  
        |------------|--------------|  
        | 1          | John Doe     |  
        | 2          | Jane Smith   |

        **Table 2: Courses**

        | Course_ID | Course_Name     | Instructor      |  
        |-----------|-----------------|-----------------|  
        | C1        | Mathematics     | Dr. Smith       |  
        | C2        | Physics         | Dr. Brown       |  

        **Table 3: Enrollments**

        | Student_ID | Course_ID |  
        |------------|-----------|  
        | 1          | C1        |  
        | 1          | C2        |  
        | 2          | C1        | 

3. `3NF` (Third  Normal Form): Extends 2NF by ensuring that no non-key attribute depends on another non-key attribute. All non-key attributes must only depend on the primary key directly.
      - **Initial Table (Not in 3NF)**:

        | Employee_ID | Employee_Name | Department_ID | Department_Name | Manager_Name  |  
        |-------------|---------------|---------------|-----------------|---------------|  
        | 1           | John Doe      | D1            | HR              | Alice Smith   |  
        | 2           | Jane Smith    | D2            | IT              | Bob Johnson   |  
        | 3           | Sam Brown     | D1            | HR              | Alice Smith   | 

      - **Issues**:
          - `Department_Name` and `Manager_Name` depend on `Department_ID`, not directly on `Employee_ID`.
          - This violates the 3NF rule that non-key attributes must depend only on the primary key.

      - **Transformed Table (In 3NF):**

        **Table 1: Employees**

        | Employee_ID | Employee_Name | Department_ID |  
        |-------------|---------------|---------------|  
        | 1           | John Doe      | D1            |  
        | 2           | Jane Smith    | D2            |  
        | 3           | Sam Brown     | D1            |

        **Table 2: Departments**

        | Department_ID | Department_Name | Manager_Name  |  
        |---------------|-----------------|---------------|  
        | D1            | HR              | Alice Smith   |  
        | D2            | IT              | Bob Johnson   |
