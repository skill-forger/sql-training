# Week 7: SQL Standards

## Table of Contents
<ol>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#objectives">Objectives</a></li>
    <li><a href="#standards-following?">Standards Following?</a></li>
    <li><a href="#sql-standards">SQL Standards</a></li>
</ol>

## Overview
This document provides guidelines for writing clean, consistent, and maintainable SQL code. 
Following these standards helps improve collaboration, readability, and code quality across projects.

## Objectives
- Ensure consistency in SQL code across the team.
- Improve code maintainability and readability.
- Facilitate easier code review and debugging.

## Standards Following?
- Example: 
  - Not following standards:
  ```sql
  SELECT employee_id,name,department_name FROM employees e JOIN departments d ON e.department_id=d.department_id WHERE e.status='Active' AND e.salary>5000 ORDER BY e.name;
  ```
  - Following standards:
  ```sql
  SELECT e.employee_id,
         e.name,
         d.department_name
  FROM employees AS e
  JOIN departments AS d 
    ON e.department_id = d.department_id
  WHERE e.status = 'Active'
  AND e.salary > 5000
  ORDER BY e.name;
  ```
- For Developers:
  - Improve code readability and maintainability.
  - Easier to collaborate on projects.
  - Reduce time spent understanding others' code.
- For Clients:
  - Consistent structure in deliverables.
  - Easier code review and testing.

## SQL Standards
1. Naming convention
   - Use descriptive, consistent names for tables, columns, and fields.
   - Avoid special characters in names such as $, &, *, %, etc. (only use letters, numbers, and underscores).
   - Do not start table names with an underscore.
   - Avoid abbreviations, always write full names according to naming conventions.
   - Name tables and columns consistently.
   - Use the keyword `AS` to create aliases.
   - Use lowercase letters for object names such as columns or tables.

2. Indentation and Alignment
   - List each column on a separate line after `SELECT`.
   - Ensure commas are placed at the end of each line.
   - Example: 
     ```sql
     SELECT p.PersonId,
            p.FirstName,
            p.LastName,
            p.Name
     FROM Person AS p
     JOIN City AS c
       ON p.CityId = c.CityId;
     ```
   - Keywords like `FROM`, `WHERE`, `ORDER BY`, `GROUP BY`, and `HAVING` should each be on a new line without indentation.
   - Example:
     ```sql
     SELECT p.PersonId,
            p.FirstName,
            p.LastName,
            p.Name
     FROM Person AS p
     WHERE p.Name = ‘New York’;
     ```
   - Separate each condition onto a new line and indentation.
   - Use a new indented line with `AND` or `OR` operators.
   - Example:
     ```sql
     SELECT p.PersonId,
            p.FirstName,
            p.LastName,
            p.Name
     FROM Person AS p
     WHERE p.Name = ‘New York’
       OR p.Name = ‘Chicago’;
     ```
3. Comments
   - Use comments to explain complex queries.
   - For multi-line comments, use `/* */`.
   - For single-line comments, use `--`.
   - Example:
     ```sql
     -- Selected column in SELECT statement
     SELECT p.PersonId, 
            p.FirstName,       
            p.LastName,         
            p.Name              
     FROM Person AS p
     WHERE p.Name = ‘New York’;
     ```
4. Join Query
   - Write each `JOIN` clause on a separate line.
   - Indent the `ON` condition under the `JOIN` statement.
   - Example:
     ```sql
     SELECT p.PersonId, 
            p.FirstName,       
            p.LastName,         
            p.Name             
     FROM Person AS p
     JOIN City AS c 
       ON p.CityId = c.CityId;
     ```
4. Subqueries
   - Subqueries should be indented under the main query.
   - Each subquery should be on a new line.
   - Example:
     ```sql
     SELECT employees.employee_id,
            total_sale.total
     FROM 
       (
         SELECT SUM(total) AS total,
                salesman_id
         FROM orders
         GROUP BY salesman_id
       ) total_sale
     JOIN employees 
       ON total_sale.salesman_id = employees.employee_id;
     ```