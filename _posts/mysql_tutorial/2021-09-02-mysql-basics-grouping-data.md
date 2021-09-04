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



