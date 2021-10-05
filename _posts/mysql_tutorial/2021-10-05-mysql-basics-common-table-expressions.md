---
layout: post
title: "Data Analysis: MySQL Basics - Common Table Expressions"
subtitle: 'Basics of Common Table Expressions'
author: "Mengran"
header-style: text
tags:
  - Data Analysis
  - MySQL
---

## Common Table Expression or CTE

A **common table expression** is a named temporary result set that exists only within the execution scope of a single SQL statement e.g.,`SELECT`, `INSERT`, `UPDATE`, or `DELETE`.

Basic Syntax:

```vim
WITH cte_name (column_list) AS (
    query
) 
SELECT * FROM cte_name;

```

### CTE Examples

Example 1:
- the name of the CTE is `customers_in_usa`, the query that defines the CTE returns two columns `customerName` and `state`.
- the`customers_in_usa` CTE returns all customers located in the USA.


```vim
WITH customers_in_usa AS (
    SELECT 
        customerName, state
    FROM
        customers
    WHERE
        country = 'USA'
) SELECT 
    customerName
 FROM
    customers_in_usa
 WHERE
    state = 'CA'
 ORDER BY customerName;

```

Example 2: Using two CTEs
- we have two CTEs in the same query.
- The first CTE ( salesrep) gets the employees whose job titles are the sales representative.
- The second CTE ( customer_salesrep ) references the first CTE in the INNER JOIN clause to get the sales rep and customers of whom each sales rep is in charge.
- After having the second CTE, we query data from that CTE using a simple SELECT statement with the ORDER BY clause.

```vim
WITH salesrep AS (
    SELECT 
        employeeNumber,
        CONCAT(firstName, ' ', lastName) AS salesrepName
    FROM
        employees
    WHERE
        jobTitle = 'Sales Rep'
),
customer_salesrep AS (
    SELECT 
        customerName, salesrepName
    FROM
        customers
            INNER JOIN
        salesrep ON employeeNumber = salesrepEmployeeNumber
)
SELECT 
    *
FROM
    customer_salesrep
ORDER BY customerName;

```

### The `WITH` Clause

a `WITH` clause can be used at the beginning of SELECT, UPDATE, and DELETE statements:

```vim
WITH ... SELECT ...
WITH ... UPDATE ...
WITH ... DELETE ...
```

a `WITH` clause can be used at the beginning of a subquery or a derived table subquery:

```vim
SELECT ... WHERE id IN (WITH ... SELECT ...);

SELECT * FROM (WITH ... SELECT ...) AS derived_table;
```

a `WITH` clause can be used immediately preceding SELECT of the statements that include a SELECT clause:

```vim
CREATE TABLE ... WITH ... SELECT ...
CREATE VIEW ... WITH ... SELECT ...
INSERT ... WITH ... SELECT ...
REPLACE ... WITH ... SELECT ...
DECLARE CURSOR ... WITH ... SELECT ...
EXPLAIN ... WITH ... SELECT ...
```






