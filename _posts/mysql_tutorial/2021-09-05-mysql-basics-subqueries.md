---
layout: post
title: "Data Analysis: MySQL Basics - Subqueries"
subtitle: 'Basics of Sub queries'
author: "Mengran"
header-style: text
tags:
  - Data Analysis
  - MySQL
---

## Subqueries

**Basic clauses:**
- `Subquery` – show you how to nest a query (inner query) within another query (outer query) and use the result of the inner query for the outer query.
- `Derived table` – introduce you to the derived table concept and show you how to use it to simplify complex queries.
- `EXISTS` – test for the existence of rows.

### Subquery

A subquery is **a query nested within another query** such as `SELECT`, `INSERT`, `UPDATE` or `DELETE`. 

Also, a subquery can be nested within another subquery.
- inner query - A subquery is called an inner query 
- outer query - a query that contains the subquery

A subquery can be used anywhere that expression is used and must be closed in parentheses.

Example: uses a subquery to return the employees who work in the offices located in the USA
- The subquery returns all office codes of the offices located in the USA.
- The outer query selects the last name and first name of employees who work in the offices whose office codes are in the result set returned by the subquery.

```vim
SELECT 
    lastName, firstName
FROM
    employees
WHERE
    officeCode IN (SELECT 
            officeCode
        FROM
            offices
        WHERE
            country = 'USA');

```

#### subquery with comparison operators

You can use **comparison operators** e.g., `=`, `>`, `<` to compare a single value returned by the subquery with the expression in the `WHERE` clause.

**Example 1: returns the customer who has the highest payment.**
```vim
SELECT 
    customerNumber, 
    checkNumber, 
    amount
FROM
    payments
WHERE
    amount = (SELECT MAX(amount) FROM payments);
    
>>>
customerNumber	checkNumber	amount
141	        JE105477	120166.58
```

**Example 2:** find customers whose payments are greater than the average payment using a subquery
- First, get the average payment by using a subquery.
- Then, select the payments that are greater than the average payment returned by the subquery in the outer query.

```vim
SELECT 
    customerNumber, 
    checkNumber, 
    amount
FROM
    payments
WHERE
    amount > (SELECT 
            AVG(amount)
        FROM
            payments);
>>>
customerNumber	checkNumber	amount
112	        HQ55022	        32641.98
112	        ND748579	33347.88
114	        GG31455	        45864.03
```

#### subquery with IN and NOT IN operators

If a subquery returns more than one value, you can use other operators such as `IN` or `NOT IN` operator in the `WHERE` clause.

Example: use a subquery with `NOT IN` operator to find the customers who have not placed any orders

```vim
SELECT 
    customerName
FROM
    customers
WHERE
    customerNumber NOT IN (SELECT DISTINCT
            customerNumber
        FROM
            orders);
>>>
customerName
Havel & Zbyszek Co
American Souvenirs Inc
Porto Imports Co.
```

#### subquery in the `FROM` clause

When you use a subquery in the `FROM` clause, the result set returned from a subquery is used as a temporary table. 

This table is referred to as a derived table or materialized subquery.

Example: finds the maximum, minimum, and average number of items in sale orders
- `FLOOR()` is used to **remove decimal places** from the average values of items

```vim
SELECT 
    MAX(items), 
    MIN(items), 
    FLOOR(AVG(items))
FROM
    (SELECT 
        orderNumber, COUNT(orderNumber) AS items
    FROM
        orderdetails
    GROUP BY orderNumber) AS lineitems;
    
>>>
MAX(items)	MIN(items)	FLOOR(AVG(items))
18	        1	        9
```

#### correlated subquery

**subquery is independent.** 

It means that you can execute the subquery **as a standalone query**.

```vim
SELECT 
    orderNumber, 
    COUNT(orderNumber) AS items
FROM
    orderdetails
GROUP BY orderNumber;

```

A **correlated subquery** is a subquery that uses the data from the outer query. 

In other words, a correlated subquery depends on the outer query. A correlated subquery is evaluated once for each row in the outer query.

**Example:** uses a **correlated subquery** to select products whose buy prices are greater than the average buy price of all products in each product line.

```vim
SELECT 
    productname, 
    buyprice
FROM
    products p1
WHERE
    buyprice > (SELECT 
            AVG(buyprice)
        FROM
            products
        WHERE
            productline = p1.productline)
>>>
productname	                buyprice
1952 Alpine Renault 1300	98.58
1996 Moto Guzzi 1100i	    68.99
```

Both outer query and correlated subquery reference the same products table. Therefore, we need to use a table alias p1 for the products table in the outer query.

Unlike a regular subquery, you cannot execute a correlated subquery independently like this. If you do so, MySQL doesn’t know the p1 table and will issue an error.
- For each row in the products (or p1) table, the correlated subquery needs to execute once to get the average buy price of all products in the productline of that row.
- If the buy price of the current row is greater than the average buy price returned by the correlated subquery, the query includes the row in the result set.

```vim
SELECT 
    AVG(buyprice)
FROM
    products
WHERE
    productline = p1.productline;
    
```

#### subquery with EXISTS and NOT EXISTS

When a subquery is used with the `EXISTS` or `NOT EXISTS` operator, a subquery returns a `Boolean` value of `TRUE` or `FALSE`. 

The following query illustrates a subquery used with the `EXISTS` operator:

```vim
SELECT 
    *
FROM
    table_name
WHERE
    EXISTS( subquery );
```

In the query above, if the subquery returns any rows, `EXISTS` subquery returns `TRUE`, otherwise, it returns `FALSE`.

The `EXISTS` and `NOT EXISTS` are often used in the correlated subqueries.

Example: finds sales orders whose total values are greater than 60K

```vim
SELECT 
    orderNumber, 
    SUM(priceEach * quantityOrdered) total
FROM
    orderdetails
        INNER JOIN
    orders USING (orderNumber)
GROUP BY orderNumber
HAVING SUM(priceEach * quantityOrdered) > 60000;

>>>
orderNumber	  total
10165	          67392.85
10287	          61402.00
10310	          61234.67
```

### Derived Tables

A **derived table** is a **virtual table** returned from a `SELECT` statement. 

A derived table is similar to a temporary table, but using a derived table in the `SELECT` statement is much simpler than a temporary table because **it does not require creating the temporary table**.

The term derived table and subquery is often used interchangeably. 

When a stand-alone subquery is used in the `FROM` clause of a `SELECT` statement, it is also called a derived table.

Unlike a subquery, a derived table **must have an alias** so that you can reference its name later in the query. 

Basic Syntax:

```vim
SELECT 
    select_list
FROM
    (SELECT 
        select_list
    FROM
        table_1) derived_table_name
WHERE 
    derived_table_name.c1 > 0;
```

Example: gets the top five products by sales revenue in 2003 from the `orders` and `orderdetails` tables, then use the result of this query as a derived table and join it with the `products` table
- First, the subquery is executed to create a result set or derived table.
- Then, the outer query is executed that joined the top5product2003 derived table with the products table using the productCode column.

```vim
SELECT 
    productName, sales
FROM
    (SELECT 
        productCode, 
        ROUND(SUM(quantityOrdered * priceEach)) sales
    FROM
        orderdetails
    INNER JOIN orders USING (orderNumber)
    WHERE
        YEAR(shippedDate) = 2003
    GROUP BY productCode
    ORDER BY sales DESC
    LIMIT 5) top5products2003
INNER JOIN
    products USING (productCode);

>>>
productName      sales
2001HelloKitty   123220
2010Hellowendy   232102
```

#### derived table example

Scenario: classify the customers who bought products in 2003 into 3 groups: platinum, gold, and silver. Also, you need to know the number of customers in each group with the following conditions:
- Platinum customers who have orders with the volume greater than 100K.
- Gold customers who have orders with the volume between 10K and 100K.
- Silver customers who have orders with the volume less than 10K.

First, need to put each customer into the respective group using `CASE` expression and `GROUP BY` clause:

```vim
SELECT 
    customerNumber,
    ROUND(SUM(quantityOrdered * priceEach)) sales,
    (CASE
        WHEN SUM(quantityOrdered * priceEach) < 10000 THEN 'Silver'
        WHEN SUM(quantityOrdered * priceEach) BETWEEN 10000 AND 100000 THEN 'Gold'
        WHEN SUM(quantityOrdered * priceEach) > 100000 THEN 'Platinum'
    END) customerGroup
FROM
    orderdetails
        INNER JOIN
    orders USING (orderNumber)
WHERE
    YEAR(shippedDate) = 2003
GROUP BY customerNumber;

>>>
customerNumber   sales   customerGroup
103              12323   Gold
112              23212   Gold
113              30403   Platinum
124              50232   Silver
...
```

Then, use this query as the derived table and perform grouping:

```vim
SELECT 
    customerGroup, 
    COUNT(cg.customerGroup) AS groupCount
FROM
    (SELECT 
        customerNumber,
            ROUND(SUM(quantityOrdered * priceEach)) sales,
            (CASE
                WHEN SUM(quantityOrdered * priceEach) < 10000 THEN 'Silver'
                WHEN SUM(quantityOrdered * priceEach) BETWEEN 10000 AND 100000 THEN 'Gold'
                WHEN SUM(quantityOrdered * priceEach) > 100000 THEN 'Platinum'
            END) customerGroup
    FROM
        orderdetails
    INNER JOIN orders USING (orderNumber)
    WHERE
        YEAR(shippedDate) = 2003
    GROUP BY customerNumber) cg
GROUP BY cg.customerGroup;    

>>>
customerGroup   groupCount
Gold            61
Silver          8
Platinum        4
```

### EXISTS

The `EXISTS` operator is a **Boolean** operator that returns either true or false. 

The `EXISTS `operator is often used to test for the existence of rows returned by the subquery.

The `EXISTS` operator terminates further processing immediately once it finds a matching row, which can help improve the performance of the query.

Basic Syntax:

```vim
SELECT 
    select_list
FROM
    a_table
WHERE
    [NOT] EXISTS(subquery);
```

Example 1: uses the `EXISTS` operator to find the customer who has at least one order
- If the `customerNumber`, which appears in the `customers` table, exists in the `orders` table, the subquery returns the first matching row. 
- As a result, the `EXISTS` operator returns true and stops examining the `orders` table. 

```vim
SELECT 
    customerNumber, 
    customerName
FROM
    customers
WHERE
    EXISTS(
	SELECT 
            1
        FROM
            orders
        WHERE
            orders.customernumber 
		= customers.customernumber);

>>>
customerNumber	customerName
103	        Atelier graphique
112	        Signal Gift Stores
114	        Australian Collectors, Co
```

Example 2: uses the `NOT EXISTS` operator to find customers who do not have any orders

```vim
SELECT 
    customerNumber, 
    customerName
FROM
    customers
WHERE
    NOT EXISTS( 
	SELECT 
            1
        FROM
            orders
        WHERE
            orders.customernumber = customers.customernumber
	);
```

#### UPDATE EXISTS

**Scenario:** have to update the phone’s extensions of the employees who work at the office in San Francisco.

First, finds employees who work at the office in `San Franciso`:

```vim
SELECT 
    employeenumber, 
    firstname, 
    lastname, 
    extension
FROM
    employees
WHERE
    EXISTS( 
        SELECT 
            1
        FROM
            offices
        WHERE
            city = 'San Francisco' AND 
           offices.officeCode = employees.officeCode);

>>>
employeenumber	firstname	lastname	extension
1002	        Diane	         Murphy	        x5800
1056	        Mary	         Patterson	x4611
1076	        Jeff	         Firrelli	x9273
```

Then, adds the number 1 to the phone extension of employees who work at the office in San Francisco:

```vim
UPDATE employees 
SET 
    extension = CONCAT(extension, '1')
WHERE
    EXISTS( 
        SELECT 
            1
        FROM
            offices
        WHERE
            city = 'San Francisco'
                AND offices.officeCode = employees.officeCode);
                
```

#### INSERT EXISTS

`INSERT EXISTS` means addddd dddddd











