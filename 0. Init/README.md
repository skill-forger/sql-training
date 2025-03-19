# Database Initiation

## Usage Guide
- Read the document to grasp the foundational theory.
- Set up practice tools as guided.
- Perform SQL queries to apply the learned knowledge.

## Installation
- RDBMS: MySQL
- References:
    - On computer: [Document](https://www.simplilearn.com/tutorials/mysql-tutorial/mysql-workbench-installation) 
    - On Docker: [Document](https://hevodata.com/learn/docker-mysql/) 

## Fundamental Knowledge
- **Why use a database?**
- **Characteristics of data in a database:**
    - Data is centrally managed.
    - Minimizes duplication and ensures consistency.
    - Data retrieval is fast.
    - Capable of storing large amounts of data.
    - Supports concurrent access.
- **Database concept:**
    - A collection of data organized and stored in a structured way to serve various purposes selectively.
    - A database allows users to search, add, edit, and delete information.
    - Example: Employee database, customer database, goods database, etc.
- **Relational database:**
    - Data is organized into interrelated tables, reducing data redundancy while ensuring efficiency in storage and retrieval.
    - **Components:**
        - **Data tables:**
            - Primary Key:
                - A property (or set of properties) in a database table that uniquely identifies each record (row).
                - Unique.
                - Cannot be empty.
                - Fixed value.
            - Column: Represents the attributes of the data table.
            - Row: Represents a related set of data.
        - **Relationships:**
            - Foreign Key: A property (or set of properties) in a table used to create relationships between that table and another. Its values must match the primary key values in the referenced table.
    - **Relational Database Management System (RDBMS):**
        - Software that provides tools for:
            - Building databases.
            - Controlling data retrieval.
            - Manipulating data.
        - Popular RDBMS: MySQL, MS SQL Server, Oracle, PostgreSQL, etc.
- **Relational database and Non relational database:**
    - **Concepts:**
      - **SQL:** A type of database that stores data in tabular format with predefined schema and uses structured query language for data manipulation.
      - **NoSQL:** A type of database that stores data in various formats such as key-value pairs, documents, graphs, or wide-column stores without requiring a fixed schema.
    - **Differences:**

    | Feature               | SQL                        | NoSQL                                                        |
    |-----------------------|----------------------------|--------------------------------------------------------------|
    | **Data Structure**    | Tables (Rows & Columns)    | Key-Value, Document, Column-Family, Graph                    |
    | **Schema**            | Fixed Schema               | Dynamic Schema                                               |
    | **Scalability**       | Vertical (Scale-Up)        | Horizontal (Scale-Out)                                       |
    | **Transactions**      | ACID Compliance            | BASE (Basically Available, Soft State, Eventual Consistency) |
    | **Performance**       | Better for complex queries | Better for large-scale, distributed data                     |
    | **Use Cases**         | Financial Systems, CRM     | IoT, Big Data, Real-Time Analytics                           |

    - **When to Use:**
        - **SQL:** 
           - Structured data with defined schemas.
           - Applications that need strong consistency.
           - Complex queries with relationships(e.g., JOIN operations across multiple tables).
           - Systems that require ACID Transactions (Atomicity, Consistency, Isolation, Durability)
        - **NoSQL:**
           - Unstructured or semi-structured data.
           - Real-time applications with high write loads.
           - Dynamic data models (e.g., user settings, social media posts).
           - Horizontal scalability.
