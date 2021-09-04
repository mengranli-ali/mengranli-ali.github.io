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






