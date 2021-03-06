---
layout: post
title: "Data Analysis: MySQL Basics - Grouping Data"
subtitle: 'Basics of Grouping data'
author: "Mengran"
header-style: text
tags:
  - Data Analysis
  - MySQL
---

## Grouping Data

**Basic Clauses:**
- `GROUP BY` – show you how to group rows into groups based on columns or expressions.
- `HAVING` – filter the groups by a specific condition.
- `ROLLUP` –  generate multiple grouping sets considering a hierarchy between columns specified in the GROUP BY clause.

### GROUP BY clause

The `GROUP BY` clause groups a set of rows into a set of summary rows by values of columns or expressions. 

The `GROUP BY` clause returns one row for each group. In other words, it reduces the number of rows in the result set.

The `GROUP BY` clause is an optional clause of the SELECT statement. 

```vim
SELECT 
    c1, c2,..., cn, aggregate_function(ci)
FROM
    table
WHERE
    where_conditions
GROUP BY c1 , c2,...,cn;
```

**`GROUP BY` example:**

To group values of the order’s status into subgroups.

```vim
SELECT 
    status
FROM
    orders
GROUP BY status;
```

#### GROUP BY with aggregate functions

The aggregate functions allow you to perform the calculation of a set of rows and return a single value. 

The `GROUP BY` clause is often used with an aggregate function to perform calculations and return a single value for each subgroup.

**Example 1: `COUNT(*)`**
- to know the number of orders in each status

```vim
SELECT 
    status, COUNT(*)
FROM
    orders
GROUP BY status;

>>>
status	        COUNT(*)
Cancelled	6
Disputed	3
In Process	6
On Hold	        4
Resolved	4
```

**Example 2: `INNER JOIN`**
- To get the total amount of all orders by status
- Use the `SUM` function to calculate the total amount

```vim
SELECT 
    status, 
    SUM(quantityOrdered * priceEach) AS amount
FROM
    orders
INNER JOIN orderdetails 
    USING (orderNumber)
GROUP BY 
    status;

>>>
status	        amount
Cancelled	238854.18
Disputed	61158.78
In Process	135271.52
```

**Example 3: `SUM(quantityOrdered * priceEach) AS total`**
- returns the order numbers and the total amount of each order.

```vim
SELECT 
    orderNumber,
    SUM(quantityOrdered * priceEach) AS total
FROM
    orderdetails
GROUP BY 
    orderNumber;

>>>
status	       COUNT(*)
Cancelled	6
Disputed	3
In Process	6
```

#### GROUP BY with expression example

You can also group rows by expressions.
- used the `YEAR` function to extract year data from order date ( `orderDate`)
- the expression which appears in the `SELECT` clause must be the same as the one in the `GROUP BY` clause

```vim
SELECT 
    YEAR(orderDate) AS year,
    SUM(quantityOrdered * priceEach) AS total
FROM
    orders
INNER JOIN orderdetails 
    USING (orderNumber)
WHERE
    status = 'Shipped'
GROUP BY 
    YEAR(orderDate);

>>>
year	total
2003	3223095.80
2004	4300602.99
2005	1341395.85
```

#### GROUP BY with HAVING clause example

To **filter the groups** returned by `GROUP BY` clause, you use a `HAVING` clause

Example:
- uses the `HAVING` clause to select the total sales of the years **after 2003**

```vim
SELECT 
    YEAR(orderDate) AS year,
    SUM(quantityOrdered * priceEach) AS total
FROM
    orders
INNER JOIN orderdetails 
    USING (orderNumber)
WHERE
    status = 'Shipped'
GROUP BY 
    year
HAVING 
    year > 2003;

>>>
year	total
2004	4300602.99
2005	1341395.85
```

#### GROUP BY clause vs. DISTINCT clause

If you use the `GROUP BY` clause in the `SELECT` statement without using aggregate functions, the `GROUP BY` clause behaves like the `DISTINCT` clause.

The difference between `DISTINCT` clause and `GROUP BY` clause is that the `GROUP BY` clause sorts the result set, whereas the `DISTINCT` clause does not.

The following statement uses the `GROUP BY` clause to select the unique states of customers from the customers table.

```vim
SELECT 
    state
FROM
    customers
GROUP BY state;

>>>
state
null
BC
CA
Co. Cork
CT
Isle o
```

Alternative:
- You can achieve a similar result by using the `DISTINCT`clause:

```vim
SELECT DISTINCT
    state
FROM
    customers;

>>>
state
null
NV
Victoria
CA
NY
PA
```

**Using `DISTINCT` clause & `GROUP BY` clause:**

If you add the `ORDER BY` clause to the statement that uses the  `DISTINCT` clause, the result set is sorted, and it is the same as the one returned by the statement that uses `GROUP BY` clause.

```vim
SELECT DISTINCT
    state
FROM
    customers
ORDER BY 
    state;

>>>
state
null
BC
CA
Co. Cork
```

### HAVING clause

The `HAVING` clause is used in the `SELECT` statement to specify filter conditions for a group of rows or aggregates.

The `HAVING` clause is often used with the `GROUP BY` clause to filter groups based on a specified condition. 

If you omit the `GROUP BY` clause, the `HAVING` clause behaves like the `WHERE` clause.

`HAVING group_condition;`

**Difference between `HAVING` clause vs `WHERE` clause:**
- the `HAVING` clause applies a filter condition to **each group of rows**
- the `WHERE` clause applies the filter condition to **each individual row**


```vim
SELECT 
    select_list
FROM 
    table_name
WHERE 
    search_condition
GROUP BY 
    group_by_expression
HAVING 
    group_condition;

```

#### `HAVING` clause example - greater than

Find which order has total sales **greater than** 1000 by using the `HAVING` clause:

```vim
SELECT 
    ordernumber,
    SUM(quantityOrdered) AS itemsCount,
    SUM(priceeach*quantityOrdered) AS total
FROM
    orderdetails
GROUP BY 
   ordernumber
HAVING 
   total > 1000;

>>>
ordernumber	itemsCount	total
10100	             151	10223.83
10101	             142	10549.01
10102	             80	        5494.78
```

#### `HAVING` clause with logical operators `OR` & `AND`.

Uses the `HAVING` clause to find orders that have **total amounts greater than** 1000 and **contain more than** 600 items:

`HAVING total > 1000 AND itemsCount > 600;`

```vim
SELECT 
    ordernumber,
    SUM(quantityOrdered) AS itemsCount,
    SUM(priceeach*quantityOrdered) AS total
FROM
    orderdetails
GROUP BY ordernumber
HAVING 
    total > 1000 AND 
    itemsCount > 600;
    
>>>
ordernumber	itemsCount	total
10106	              675	52151.81
10126	              617	57131.92
10135	              607	55601.84
```

To find all orders that already shipped and have a total amount greater than 1500:
- you can join the `orderdetails `table with the orders table using the `INNER JOIN` clause and apply a condition on `status` column and `total` aggregate

```vim
SELECT 
    a.ordernumber, 
    status, 
    SUM(priceeach*quantityOrdered) total
FROM
    orderdetails a
INNER JOIN orders b 
    ON b.ordernumber = a.ordernumber
GROUP BY  
    ordernumber, 
    status
HAVING 
    status = 'Shipped' AND 
    total > 1500;

>>>
ordernumber	status	    total
10100	        Shipped	    10223.83
10101	        Shipped	    10549.01
10102	        Shipped	    5494.78
```

### ROLLUP clause

You can use the `ROLLUP` clause to **generate subtotals and grand totals**.

First, setup a sample table:
- creates a new table named `sales` that stores the order values summarized by product lines and years.
- ehe data comes from the `products`, `orders`, and `orderDetails` tables in the sample database.

```vim
CREATE TABLE sales
SELECT
    productLine,
    YEAR(orderDate) orderYear,
    SUM(quantityOrdered * priceEach) orderValue
FROM
    orderDetails
        INNER JOIN
    orders USING (orderNumber)
        INNER JOIN
    products USING (productCode)
GROUP BY
    productLine ,
    YEAR(orderDate);

>>>

```

```vim
SELECT * FROM sales;

>>>
productLine   orderYear  orderValue
Classic Cars  2010       4080.00
Trains        2011       2770.00
Motorcycles   2011       1323.00
Vintage Cars  2012       5022.00
```

Secondly, **a grouping set** is a set of columns to which you want to group. 

For example, the following query creates a grouping set denoted by (`productline`):

```vim
SELECT 
    productline, 
    SUM(orderValue) totalOrderValue
FROM
    sales
GROUP BY 
    productline;

>>>
productLine   totalOrderValue
Classic Cars  15434.00
Trains        13232.00
Motorcycles   10445.00
Vintage Cars  9922.00
```

Then creates an empty grouping set denoted by the `()`:
```vim
SELECT 
    SUM(orderValue) totalOrderValue
FROM
    sales;

>>>
totalOrderValue
89022.69
```

To generate **two or more grouping sets** together in one query, you may use the `UNION ALL` operator:
- The `NULL` in the productLine column identifies the **grand total super-aggregate line**.

```vim
SELECT 
    productline, 
    SUM(orderValue) totalOrderValue
FROM
    sales
GROUP BY 
    productline 
UNION ALL
SELECT 
    NULL, 
    SUM(orderValue) totalOrderValue
FROM
    sales;

>>>
productLine   totalOrderValue
Classic Cars  15434.00
Trains        13232.00
Motorcycles   10445.00
Vintage Cars  9922.00
...
null          89022.69
```

**Solution: use `ROLLUP` clause**

The `ROLLUP` clause is an extension of the `GROUP BY` clause with the following syntax:

```vim
SELECT 
    select_list
FROM 
    table_name
GROUP BY
    c1, c2, c3 WITH ROLLUP;
```

The `ROLLUP` generates **multiple grouping sets** based on the columns or expressions specified in the GROUP BY clause:

It generates not only the subtotals but also the grand total of the order values.

```vim
SELECT 
    productLine, 
    SUM(orderValue) totalOrderValue
FROM
    sales
GROUP BY 
    productline WITH ROLLUP;
    
>>>
productLine   totalOrderValue
Classic Cars  15434.00
Trains        13232.00
Motorcycles   10445.00
Vintage Cars  9922.00
...
null          89022.69
```

**`ROLLUP` clause with hierarchy**

Basic syntax:

`GROUP BY c1, c2, c3 WITH ROLLUP`

Then the hierarchy is as below:

`c1 > c2 > c3`

Then the subtotal will be based off `c1`

Example:
- In this case,` productLine > orderYear`
- If you reverse it to `GROUP BY orderYear, productline WITH ROLLUP;` it will be `orderYear > productLine`, which means calculating the subtotal of total order value for each year group

```vim
SELECT 
    productLine, 
    orderYear,
    SUM(orderValue) totalOrderValue
FROM
    sales
GROUP BY 
    productline, 
    orderYear 
WITH ROLLUP;

>>>
productLine   orderYear   totalOrderValue
Classic Cars  2012        10000.00
Classic Cars  2013        11000.00
Classic Cars  2014        12000.00
Classic Cars  null        33000.00
Trains        2012        15000.00
Trains        2014        15000.00
Trains        2015        15000.00
Trains        null        45000.00
...
null          null        78000.00
```

#### GROUPING() function

Use the `GROUPING()` function to check whether `NULL` in the result set represents the subtotals or grand totals.

The `GROUPING()` function returns 1 when `NULL` occurs in a supper-aggregate row, otherwise, it returns 0.

```vim
SELECT 
    IF(GROUPING(orderYear),
        'All Years',
        orderYear) orderYear,
    IF(GROUPING(productLine),
        'All Product Lines',
        productLine) productLine,
    SUM(orderValue) totalOrderValue
FROM
    sales
GROUP BY 
    orderYear , 
    productline 
WITH ROLLUP;

>>>
orderYear    productLine         totalOrderValue
2010         Classic Cars        10000.00
2010         Motorcycles         5000.00
2010         Trains              8000.00
2010         All Product Lines   23000.00
2011         Classic Cars        20000.00
2011         Motorcycles         8000.00
2011         Trains              9000.00
2011         All Product Lines   37000.00
All Years    All Product Lines   60000.00         
```







