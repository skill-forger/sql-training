# Week 8: Transaction

## Table of Contents
<ol>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#objectives">Objectives</a></li>
    <li><a href="#definition">Definition</a></li>
    <li><a href="#why-use-transaction">Why Use Transaction</a></li>
    <li><a href="#using-transaction">Using Transaction</a></li>
    <li><a href="#transaction-types">Transaction Types</a></li>
</ol>

## Overview
This chapter introduces transactions in MySQL, explaining their role in maintaining data integrity and ensuring atomicity, consistency, isolation, and durability (ACID properties) in database operations.

## Objectives
- Understand transactions and their importance in database management.
- Use transaction control statements (START TRANSACTION, COMMIT, ROLLBACK, SAVEPOINT).
- Ensure data consistency using ACID principles.

## Definition
- A database transaction is a series of operations executed as a single, all-or-nothing unit of work.
- All the operations inside a transaction must be completed; otherwise, it will roll back to the previous state before the operations took place.
- Very important in securing data integrity, consistency, and reliability for database systems.

## Why Use Transaction
- Example: To transfer $800 from Jane's **checking account** to her **savings account**.
- Transactional techniques allow assurance of either both actions' success or neither.
- Important in banking, e-commerce, etc applications.
- Managing errors gracefully and system failures.

## Using Transaction
- Start of a Transaction
    - The `START TRANSACTION` statement be used to start a transaction.
    - Syntax:
      ```sql
      START TRANSACTION;
      ```
- Commit a Transaction
    - The `COMMIT` statement saves all the changes made during a transaction.
    - It makes all of the changes permanent and terminates the transaction.
    - Syntax:
      ```sql
      COMMIT;
      ```
- Roll Back a Transaction
    - The `ROLLBACK` statement restores the database to its state before the transaction started.
    - Syntax:
      ```sql
      ROLLBACK;
      ```
- Savepoint:
    - Partial transaction rollbacks.
    - Syntax:
      ```sql
      SAVEPOINT <SAVEPOINT_NAME>;
      ```
    - Example:
      ```sql
      SAVEPOINT SP1;
      -- Savepoint created.
      DELETE FROM Student WHERE AGE = 20;
      -- deleted
      SAVEPOINT SP2;
      -- Savepoint created.
      ```
- Example: To transfer $800 from Jane's **checking account** to her **savings account**.
  ```sql
  START TRANSACTION;
  SELECT balance FROM checking WHERE customer_id = 888;
  UPDATE checking SET balance = balance - 800.00 WHERE customer_id = 888;
  UPDATE savings  SET balance = balance + 800.00 WHERE customer_id = 888;
  COMMIT;
  ```

## Transaction Types
- **Read Transactions**: Used to only read the data, typically with `SELECT` queries.
- **Write Transactions**: These involve modifying the data in the database with `INSERT`, `UPDATE`, or `DELETE` operations.
- **Distributed Transactions**: These transactions span multiple databases and ensure consistency across them.
- **Implicit Transactions**: Automatically started by SQL Server for certain operations.
- **Explicit Transactions**: Manually controlled transactions where the user begins and ends the transaction using `BEGIN TRANSACTION`, `COMMIT`, and `ROLLBACK`.

## ACID Properties
- ACID is a set of properties of transactions in a database management system (DBMS) that ensures data integrity in case of errors, power failures, and other risks.
- **Atomicity**: Ensures that a transaction is either fully completed or fully rolled back. No partial execution is allowed.
- **Consistency**: Guarantees that the database remains in a valid state before and after a transaction.
- **Isolation**: Ensures that concurrent transactions do not interfere with each other.
- **Durability**: Ensures that once a transaction is committed, its changes are permanently saved, even in case of a system crash.
- More details: [Document](https://www.freecodecamp.org/news/acid-databases-explained/)