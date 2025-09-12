# Module 06: Subquery, View, CTE

## Table of Contents
<ol>
    <li><a href="#objectives">Objectives</a></li>
    <li><a href="#subquery">Subquery</a></li>
    <li><a href="#view">View</a></li>
    <li><a href="#common-table-expression-cte">Common Table Expression (CTE)</a></li>
    <li><a href="#exercises">Exercises</a></li>
</ol>

## Overview
- This chapter introduces the concept of Subquery, View, Common Table Expression (CTE) and how to use them to enhance the functionality of queries.
- These techniques help improve query readability, maintainability, and performance by structuring data retrieval efficiently.
- They allow for modular query design, reducing redundancy and simplifying complex operations.
- Understanding their use cases enables better data organization, optimized execution plans, and improved database performance.

## Objectives
- Understand how to use Subqueries, Views, and CTEs to structure and optimize SQL queries.
- Learn when to apply each technique to improve query readability, maintainability, and performance. 
- Gain insights into reducing redundancy and enhancing data retrieval efficiency through modular query design.

## Subquery
- Subquery can be defined as a query embedded within another query. It is often used in the `WHERE`, `HAVING`, or `FROM` clauses of a statement. 
- Subqueries are commonly used with `SELECT`, `UPDATE`, `INSERT`, and `DELETE` statements to achieve complex filtering and data manipulation.


**Key Characteristics of Subqueries**
- **Nested Structure**: A subquery is executed within the context of an outer query.
- **Parentheses**: Subqueries must always be enclosed in parentheses.
- **Comparison Operators**: Subqueries can be used with operators like =, >, <, `IN`, `NOT IN`, `LIKE`, etc.
- **Single-Row vs. Multi-Row Subqueries**: Subqueries may return a single value (e.g., a single row) or multiple values.

For further detail can refer [here](https://www.geeksforgeeks.org/sql-subquery/).

```sql
SELECT <List of Column>
FROM <List of Table>
WHERE OPERATOR (
    SELECT <List of Column>
    FROM <List of Table>
    [WHERE]
);
```
### 1. Subquery used as an expression
- If the subquery returns a single value, it can be used anywhere the expression is used

**Example**: Find orders with the highest value for each customer

```sql
SELECT 
    customer_id,
    name as customer_name, 
    (SELECT MAX (o.total) 
        FROM orders o 
        WHERE cst.customer_id = o.customer_id
    ) AS max_total
FROM customers cst 
LEFT JOIN contacts conts 
ORDER BY customer_id DESC;

```

### 2. Subquery with operator
- Subqueries are used with operators that return one or a set of values.
- After the subquery returns values, the outer query uses them.

**Example**: Get products with highest price
```sql
SELECT 
product_id,  
product_name,  
list_price
FROM products 
WHERE list_price = 
(
    SELECT MAX (list_price)
    FROM products
);
```

**Example**: Subquery with `IN` operator

Retrieve all products with the categories 'CPU' and 'Mother Board'

```sql
SELECT 
product_id,  
product_name
FROM products 
WHERE category_id IN (
    SELECT category_id
    FROM product_categories
    WHERE category_name = 'CPU'
    OR category_name = 'Mother Board'
);
```

**Example**: Subquery with `EXISTS` (`NOT EXISTS`) operator

Get customers who purchased products in 2024

```sql
SELECT customer_id, name
FROM customers c 
WHERE EXISTS (
    SELECT customer_id
    FROM orders o
    WHERE o.customer_id = c.customer_id
    AND EXTRACT (YEAR FROM o.order_date) = 2024
);
```

### 3. Subquery in the FROM clause
- When subqueries are used in the `FROM` clause, they act as a temporary table that we can
use to join other tables
- The query that you place in the `FROM` clause must have a table alias.

**Example**: Get the total value of orders sold by employee
```sql
SELECT 
employees.employee_id, 
total_sale.total
FROM employees 
JOIN (
    SELECT sum(total) as total, salesman_id
    FROM orders
    GROUP BY salesman_id) total_sale
ON total_sale.salesman_id = employees.employee_id;
```

## View
- Views in SQL are a type of virtual table that simplifies how users interact with data across one or more tables. Unlike traditional tables, a view in SQL does not store data on disk. Instead, it dynamically retrieves data based on a pre-defined query each time it’s accessed.

For further detail can refer [here](https://www.geeksforgeeks.org/sql-views/).

### Create view

```sql
CREATE VIEW view_name AS
SELECT column1, column2…..
FROM table_name
WHERE condition;
```

**Example**: Create a view with data of all customer orders with credit limit >= 400
```sql
CREATE VIEW cust_orders AS
SELECT 
customers.customer_id, 
customers.name  
FROM customers
INNER JOIN orders ON customers.customer_id = orders.customer_id
WHERE customers.credit_limit >= 400;
```

### Update view
- If you want to update the existing data within the view, use the `UPDATE` statement.
```sql
UPDATE view_name
SET column1 = value1, column2 = value2...., columnN = valueN
WHERE [condition];
```
**Note**: Not all views can be updated using the `UPDATE` statement.


- If you want to update the view definition without affecting the data, use the `CREATE OR REPLACE VIEW` statement. you can use this syntax

```sql
CREATE OR REPLACE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

### Delete view
- SQL allows us to delete an existing View. We can delete or drop View using the DROP statement.

```sql
DROP VIEW view_name;
```

### Query data in view
- Querying data in a view is similar to querying a table.

```sql
SELECT <column_name>    
FROM <view_name>;
```

```sql
SELECT * FROM cust_orders
```

## Common Table Expression (CTE)

- **Common Table Expression (CTE)** in SQL is a temporary result set that is defined and used within the execution scope of a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement.
- CTEs are defined using the `WITH` clause and can be referenced multiple times within the main SQL query. 
- This makes CTEs a great alternative to subqueries, especially in cases where we need to perform the same operation multiple times or create recursive queries.

For further detail can refer [here](https://www.geeksforgeeks.org/sql-with-clause/).

```sql
WITH <subquery_name> AS
(
    SELECT <column_name>
    FROM <table_name>
    [WHERE conditions]
)
SELECT <column_name>
FROM <subquery_name>;
```

**Example**: For each employee, we want to know how many people work in their department.
```sql
WITH dept_count AS
(
    SELECT job_title,
    COUNT(*) dept_count
    FROM employees
    GROUP BY job_title
)
SELECT e.first_name || ' ' || e.last_name, dc.dept_count
FROM employees e, dept_count dc
WHERE e.job_title = dc.job_title;
```

## Exercises
**We have these following tables as below**

| Table                | Description                                         | Note                                          |
|----------------------|-----------------------------------------------------|-----------------------------------------------|
| `employees`          | Employees information                               |                                               |
| `customers`          | Customers information                               |                                               |
| `contacts`           | Customers contacts                                  |                                               |
| `products`           | Product information                                 |                                               |
| `product_categories` | Product categories                                  | Link to table `products` using **product_id** |
| `orders`             | Order information                                   |                                               |
| `order_items`        | Detail of each order(product, quantity, price,..s.) | Link to table `orders` using **order_id**     |

### Database Diagram
![database_diagram](../02.%20Query/images/diagram_chap2.png "database diagram")

1. Get product information and average selling price of those products.
2. Retrieve products that have never been sold.
3. Retrieve products that are currently out of stock.
4. Retrieve customers who have made purchases between 2023 and 2024.
5. Retrieve customers who have never made purchases in 2024.
6. Find all customers with a credit limit higher than the average credit limit of all customers.
7.  Retrieve customer information (Customer ID, Customer Name) for those who have made purchases with a total quantity per order exceeding 50 units and an order date later than 14/02/2024.
8. Identify the customer with the highest revenue from the above list.
9. Create a query revenue_product to retrieve Product ID, Product Name, and Revenue (total sales amount of that product).
10. Create a query to calculate the total revenue of all products.
11. Return the following result: Product ID, Product Name, Revenue, and Revenue Percentage (Revenue / Total Revenue).
12. Create a view named `cst_order` to retrieve customer information (Customer ID, Customer Name) and pending orders with a total quantity per order exceeding 50 units and an order date later than 14/02/2024. Sort the results by customer.
13. Create a view named `cst_order` to retrieve the top 100 products with the lowest stock across all countries (Product ID, Product Name, Warehouse Name, Warehouse Country, and Total Stock in Warehouse).





