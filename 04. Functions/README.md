# Module 04: Functions

## Table of Contents

<ol>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#objectives">Objectives</a></li>
    <li><a href="#numeric-functions">Numeric Functions</a></li>
    <li><a href="#string-functions">String Functions</a></li>
    <li><a href="#date-and-time-functions">Date and Time Functions</a></li>
    <li><a href="#aggregate-functions">Aggregate Functions</a></li>
    <li><a href="#exercises">Exercises</a></li>
</ol>

## Overview

- This chapter introduces the concept of SQL functions and how to use them to enhance the functionality of queries.
- Functions simplify complex operations by encapsulating reusable logic and can transform, aggregate, or analyze data
  effectively.
- SQL Functions are used to perform different operations on the database.

## Objectives

- Basic understand about SQL Functions
- Explore different types of functions
- Apply and combine built-in SQL functions to queries

## Numeric Functions

MySQL numeric functions are used primarily for numeric manipulation and/or mathematical calculations.
The following table list out some of the common numeric functions that are available in the MySQL.

For further detail can refer [here](https://dev.mysql.com/doc/refman/8.4/en/numeric-functions.html).

| Command        | Description                                                                                                                                                                                            | Syntax                                   |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------|
| **ABS()**      | Returns the absolute value of numeric expression                                                                                                                                                       | SELECT ABS(x) AS result;                 |
| **CEIL()**     | Returns the smallest integer value that is not less than passed numeric expression                                                                                                                     | SELECT CEIL(22.3) AS result;             |
| **FLOOR()**    | Returns the largest integer value that is not greater than passed numeric expression                                                                                                                   | SELECT FLOOR(22.3) AS result;            |
| **POW()**      | Returns the value of one expression raised to the power of another expression                                                                                                                          | SELECT POW(2, 3) AS result;              |
| **ROUND()**    | Returns numeric expression rounded to an integer. This function accepts two parameters: the numeric expression to be rounded, and an optional second parameter specifying the number of decimal places | SELECT ROUND(5.6523, 2) AS result;       |
| **SQRT()**     | Returns the non-negative square root of numeric expression                                                                                                                                             | SELECT SQRT(144) AS result;              |
| **TRUNCATE()** | Returns numeric exp1 truncated to exp2 decimal places. If exp2 is 0, then the result will have no decimal point                                                                                        | SELECT TRUNCATE(225.33654, 3) AS result; |

## String Functions

MySQL string functions are used to manipulate the string values. The following table list out some of the common string
functions that are available in the MySQL.

For further detail can refer [here](https://dev.mysql.com/doc/refman/8.4/en/string-functions.html).

| Command       | Description                                                                        | Syntax                                                                                |
|---------------|------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| **CONCAT()**  | Returns concatenated string                                                        | SELECT CONCAT('hello', 'world');                                                      |
| **LENGTH()**  | Returns the length of a string in bytes                                            | SELECT LENGTH('hello world');                                                         |
| **LOWER()**   | Returns the argument in lowercase                                                  | SELECT LOWER('HELLO');                                                                |
| **UPPER()**   | Returns the argument in uppercase                                                  | SELECT UPPER('hello');                                                                |
| **REPLACE()** | Replaces the matched sub string with the replacement string and returns the result | REPLACE(str,from_str,to_str) <br/>SELECT REPLACE('Hello how are you', 'Hello', 'Hi'); |

## Date and Time Functions

Date and Time functions in SQL are used to manipulate and transform date and time data stored in tables. Date functions
operate on values of the DATE datatype.

For further detail can refer [here](https://dev.mysql.com/doc/refman/8.4/en/date-and-time-functions.html).

| Command            | Description                                                                                                                                                           | Syntax                                                  |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| **ADDDATE()**      | Used to add the specified interval to a date value                                                                                                                    | SELECT ADDDATE('2008-01-02', 31);                       |
| **CURRENT_DATE()** | Used to get the current day's date                                                                                                                                    | SELECT CURDATE();                                       |
| **DATE_FORMAT()**  | This function accepts a date or date-time value and a format string as parameters. It formats the given date according to the specified format and returns the result | SELECT DATE_FORMAT('2025-01-13', '%W %M %Y') AS result; |
| **DATEDIFF()**     | Used to calculate the difference in days between two dates. It takes two date expressions as arguments and returns the number of days between them                    | SELECT DATEDIFF('2025-01-13', '2025-02-20') AS result;  |
| **NOW()**          | Returns the current date and time                                                                                                                                     | SELECT NOW() AS result;                                 |

## Aggregate Functions

SQL Aggregate Functions operate on a data group and return a singular output. They are mostly used with the GROUP BY
clause to summarize data.

For further detail can refer [here](https://dev.mysql.com/doc/refman/8.4/en/aggregate-functions-and-modifiers.html).

| Command     | Description                                            | Syntax                                     |
|-------------|--------------------------------------------------------|--------------------------------------------|
| **AVG()**   | Calculates the average value                           | SELECT AVG(column_name) FROM table_name;   |
| **COUNT()** | Counts the number of rows                              | SELECT COUNT(column_name) FROM table_name; |
| **MAX()**   | Retrieves the maximum value from a column              | SELECT MAX(column_name) FROM table_name;   |
| **MIN()**   | Retrieves the minimum value from a column              | SELECT MIN(column_name) FROM table_name;   |
| **SUM()**   | Calculates the total sum of values in a numeric column | SELECT SUM(column_name) FROM table_name;   |
| **FIRST()** | Returns the first value in an ordered set of values    | SELECT FIRST(column_name) FROM table_name; |
| **LAST()**  | Returns the last value in an ordered set of values     | SELECT LAST(column_name) FROM table_name;  |

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

1. Get all information in table `customers`
2. Convert customer name to **uppercase** and address to **lowercase**
3. Find total, maximum, minimum, average price of orders
4. Find average price of all orders sold in 2024
5. Find total price of all orders sold from 2020 to 2024
6. Find total, maximum, minimum, average price of orders with status `Pending`
7. Find total, maximum, minimum, average price of orders with status `Shipped` and order date greater than 1/1/2024
8. Find total (round up to first number in decimal), maximum, minimum, average price of orders with status `Shipped` and
   order date greater than 1/1/2024
9. Find customer id(s) have more than 4 times buying successfully (have order with status `Shipped`)
10. Find customer id(s) have more than 2 order in 2024
11. Find total, maximum, minimum, average of `list_price` by each category (using `category_id`)
12. Find total income by each month in 2024
13. Find total income by each month, year from 2023 to 2024
14. Find top 3 customers with highest order value in 2024
15. Find the Top 3 products with the lowest total sales quantity





