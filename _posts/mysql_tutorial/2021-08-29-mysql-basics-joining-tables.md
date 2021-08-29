---
layout: post
title: "Data Analysis: MySQL Basics - Joining Tables"
subtitle: 'Basics of using joining tables'
author: "Mengran"
header-style: text
tags:
  - Data Analysis
  - MySQL
---

## Joining Tables

**Basic statements of Joining Tables:**
- `Table & Column Aliases` – introduce you to table and column aliases.
- `Joins`  – give you an overview of joins supported in MySQL including inner join, left join, and right join.
- `INNER JOIN` – query rows from a table that has matching rows in another table.
- `LEFT JOIN` – return all rows from the left table and matching rows from the right table or null if no matching rows found in the right table.
- `RIGHT JOIN` – return all rows from the right table and matching rows from the left table or null if no matching rows found in the left table.
- `CROSS JOIN` – make a Cartesian product of rows from multiple tables.
- `Self-join` – join a table to itself using table alias and connect rows within the same table using inner join and left join.

### alias for columns

To give a column a descriptive name, you can use a column alias.

To assign an alias to a column, you use the `AS` keyword followed by the alias.

```vim
SELECT 
   [column_1 | expression] AS descriptive_name
FROM table_name;
```


Example - Normal statement:
- But it is quite difficult to read

```vim
SELECT 
    CONCAT_WS(', ', lastName, firstname)
FROM
    employees;
```

Using alias as a better option:

```vim
SELECT
   CONCAT_WS(', ', lastName, firstname) AS `Full name`
FROM
   employees;

>>>
Full name
Bondur, Gerard
Bondur, Loui
Bott, Larry
```

More advanced statement:
- Order by alias

```vim
SELECT
	CONCAT_WS(', ', lastName, firstname) `Full name`
FROM
	employees
ORDER BY
	`Full name`;
```

Uses column aliases in `GROUP BY` and `HAVING` clauses:
- Selects the orders whose total amount is greater than 60000.

```vim
SELECT
	orderNumber `Order no.`,
	SUM(priceEach * quantityOrdered) total
FROM
	orderDetails
GROUP BY
	`Order no.`
HAVING
	total > 60000;

>>>
Order no.	Total
10165	        67392.85
10287	        61402.00
10310	        61234.67
```

**MySQL alias for tables**

```vim
SELECT 
    e.firstName, 
    e.lastName
FROM
    employees e
ORDER BY e.firstName;

```

### join clauses

A `join` is a method of **linking data** between one (self-join) or more tables based on values of the common column between the tables.

MySQL supports the following types of joins:
- `Inner join`
- `Left join`
- `Right join`
- `Cross join`

**Sample:**

1.Create two tables called `members `and `committees`:

```vim
CREATE TABLE members (
    member_id INT AUTO_INCREMENT,
    name VARCHAR(100),
    PRIMARY KEY (member_id)
);

CREATE TABLE committees (
    committee_id INT AUTO_INCREMENT,
    name VARCHAR(100),
    PRIMARY KEY (committee_id)
);
```

2.Insert some rows into the tables `members` and `committees`:

```vim
INSERT INTO members(name)
VALUES('John'),('Jane'),('Mary'),('David'),('Amelia');

INSERT INTO committees(name)
VALUES('John'),('Mary'),('Amelia'),('Joe');
```

3.Query data from the tables `members` and `committees`:

```vim
SELECT * FROM members;

>>>
+-----------+--------+
| member_id | name   |
+-----------+--------+
|         1 | John   |
|         2 | Jane   |
|         3 | Mary   |
|         4 | David  |
|         5 | Amelia |
+-----------+--------+

SELECT * FROM committees;

>>>
+--------------+--------+
| committee_id | name   |
+--------------+--------+
|            1 | John   |
|            2 | Mary   |
|            3 | Amelia |
|            4 | Joe    |
+--------------+--------+
```

### INNER JOIN clause

The `INNER JOIN` matches each row in one table with every row in other tables and allows you to query rows that contain columns from both tables.

Basic syntax of the `inner join` clause that **joins two tables** `table_1` and `table_2`:

```vim
SELECT column_list
FROM table_1
INNER JOIN table_2 ON join_condition;
```

Uses an `inner join` clause to find members who are also the committee members:
- use the values in the name columns in both tables `members` and `committees` to match.
- `name` is the `foreign key` column in these two tables. You join tables that have foreign key relationships. 
```vim
SELECT 
    m.member_id, 
    m.name AS member, 
    c.committee_id, 
    c.name AS committee
FROM
    members m
INNER JOIN committees c ON c.name = m.name;

>>>
+-----------+--------+--------------+-----------+
| member_id | member | committee_id | committee |
+-----------+--------+--------------+-----------+
|         1 | John   |            1 | John      |
|         3 | Mary   |            2 | Mary      |
|         5 | Amelia |            3 | Amelia    |
+-----------+--------+--------------+-----------+
```

Another example:
- to get the `productCode` and `productName` from the `products` table.
- to get the `textDescription` of product lines from the `productlines` table.
- the column `productLine` in the table `products` is called the `foreign key` column.

```vim
SELECT 
    productCode, 
    productName, 
    textDescription
FROM
    products t1
INNER JOIN productlines t2 
    ON t1.productline = t2.productline;

>>>
productCode	productName	                textDescription
S10_1949	1952 Alpine Renault 1300	Attention car enthusiasts: Make your wildest car ownership dreams come true. Whether you are looking for classic muscle cars, dream sports cars or movie-inspired miniatures, you will find great choices in this category. These replicas feature superb attention to detail and craftsmanship and offer features such as working steering system, opening forward compartment, opening rear trunk with removable spare wheel, 4-wheel independent spring suspension, and so on. The models range in size from 1:10 to 1:24 scale and include numerous limited edition and several out-of-production vehicles. All models include a certificate of authenticity from their manufacturers and come fully assembled and ready for display in the home or office.
S10_4757	1972 Alfa Romeo GTA	A       Attention car enthusiasts: Make your wildest car ownership dreams come true. Whether you are looking for classic muscle cars, dream sports cars or movie-inspired miniatures, you will find great choices in this category. These replicas feature superb attention to detail and craftsmanship and offer features such as working steering system, opening forward compartment, opening rear trunk with removable spare wheel, 4-wheel independent spring suspension, and so on. The models range in size from 1:10 to 1:24 scale and include numerous limited edition and several out-of-production vehicles. All models include a certificate of authenticity from their manufacturers and come fully assembled and ready for display in the home or office.
S10_4962	1962 LanciaA Delta 16V	    Attention car enthusiasts: Make your wildest car ownership dreams come true. Whether you are looking for classic muscle cars, dream sports cars or movie-inspired miniatures, you will find great choices in this category. These replicas feature superb attention to detail and craftsmanship and offer features such as working steering system, opening forward compartment, opening rear trunk with removable spare wheel, 4-wheel independent spring suspension, and so on. The models range in size from 1:10 to 1:24 scale and include numerous limited edition and several out-of-production vehicles. All models include a certificate of authenticity from their manufacturers and come fully assembled and ready for display in the home or office.
S12_1099	1968 Ford Mustang	        Attention car ent
```

If the join condition uses the equality operator (`=`) and **the column names in both tables used for matching are the same**, and you can use the `USING` clause instead:

```vim
SELECT column_list
FROM table_1
INNER JOIN table_2 USING (column_name);
```

```vim
SELECT 
    m.member_id, 
    m.name AS member, 
    c.committee_id, 
    c.name AS committee
FROM
    members m
INNER JOIN committees c USING(name);
```

Another example:

```vim
SELECT 
    productCode, 
    productName, 
    textDescription
FROM
    products
INNER JOIN productlines USING (productline);
```

#### INNER JOIN – join multiple tables

This query uses two `INNER JOIN` clauses to join three tables: `orders`, `orderdetails`, and `products`:

```vim
SELECT 
    orderNumber,
    orderDate,
    orderLineNumber,
    productName,
    quantityOrdered,
    priceEach
FROM
    orders
INNER JOIN
    orderdetails USING (orderNumber)
INNER JOIN
    products USING (productCode)
ORDER BY 
    orderNumber, 
    orderLineNumber;

>>>
RESULT
orderNumber	orderDate	orderLineNumber	productName	                        quantityOrdered	priceEach
10100	        2003-01-06	1	        1936 Mercedes Benz 500k Roadster	49	        35.29
10100	        2003-01-06	2	        1911 Ford Town Car	                50	        55.09
10100	        2003-01-06	3	        1917 Grand Touring Sedan	        30	        136.00
10100	        2003-01-06	4	        1932 Alfa Romeo 8C2300 Spider Sport	22	        75.46
10101	        2003-01-09	1	        1928 Mercedes-Benz SSK	                26	        167.06

```

#### INNER JOIN using other operators

In addition to the equal operator (`=`), you can use other operators to form the join condition:
- greater than ( `>` )
- less than ( `<` )
- not-equal ( `<>` ) operator 

Example: uses a less-than ( `<` ) join to find the sales price of the product whose code is `S10_1678` that is less than the manufacturer’s suggested retail price (`MSRP`) for that product.

```vim
SELECT 
    orderNumber, 
    productName, 
    msrp, 
    priceEach
FROM
    products p
INNER JOIN orderdetails o 
   ON p.productcode = o.productcode
      AND p.msrp > o.priceEach
WHERE
    p.productcode = 'S10_1678';

>>>
orderNumber	productName	                        msrp	priceEach
10107	        1969 Davidson Ultimate Chopper	95.70	81.35
10121	        1969 Davidson Ultimate Chopper	95.70	86.13
10134	        1969 Davidson Ultimate Chopper	95.70	90.92
```


### LEFT JOIN clause

The **left join** selects data starting from the left table. For each row in the left table, the left join compares with every row in the right table.

The left join **selects all data from the left table** whether there are matching rows exist in the right table or not.

Basic syntax:

```vim
SELECT column_list 
FROM table_1 
LEFT JOIN table_2 ON join_condition;
```

```vim
SELECT column_list 
FROM table_1 
LEFT JOIN table_2 USING (column_name);
```

Example:

```vim
SELECT 
    m.member_id, 
    m.name AS member, 
    c.committee_id, 
    c.name AS committee
FROM
    members m
LEFT JOIN committees c USING(name);

>>>
+-----------+--------+--------------+-----------+
| member_id | member | committee_id | committee |
+-----------+--------+--------------+-----------+
|         1 | John   |            1 | John      |
|         2 | Jane   |         NULL | NULL      |
|         3 | Mary   |            2 | Mary      |
|         4 | David  |         NULL | NULL      |
|         5 | Amelia |            3 | Amelia    |
+-----------+--------+--------------+-----------+
```


Add a `WHERE` clause and `IS NULL` operator:
- To find members who are not the committee members
- This query pattern can find rows in the left table that **do not have corresponding rows** in the right table.
- Illustrates how to use the left join to select rows that only exist in the left table

```vim
SELECT 
    m.member_id, 
    m.name AS member, 
    c.committee_id, 
    c.name AS committee
FROM
    members m
LEFT JOIN committees c USING(name)
WHERE c.committee_id IS NULL;

>>>
+-----------+--------+--------------+-----------+
| member_id | member | committee_id | committee |
+-----------+--------+--------------+-----------+
|         2 | Jane   |         NULL | NULL      |
|         4 | David  |         NULL | NULL      |
+-----------+--------+--------------+-----------+
```

### RIGHT JOIN clause

The `right join` clause is similar to the left join clause except that the treatment of left and right tables is reversed. 

The `right join` starts selecting data from the right table instead of the left table.

The `right join` clause selects all rows from the right table and matches rows in the left table. If a row from the right table does not have matching rows from the left table, the column of the left table will have `NULL` in the final result set.

**Basic syntax:**

```vim
SELECT column_list 
FROM table_1 
RIGHT JOIN table_2 ON join_condition;
```

```vim
SELECT column_list 
FROM table_1 
RIGHT JOIN table_2 USING (column_name);
```

**To find rows in the right table that does not have corresponding rows in the left table:**

```vim
SELECT column_list 
FROM table_1 
RIGHT JOIN table_2 USING (column_name)
WHERE column_table_1 IS NULL;
```

**Example:**

1.uses the right join to join the `members` and `committees` tables:

```vim
SELECT 
    m.member_id, 
    m.name AS member, 
    c.committee_id, 
    c.name AS committee
FROM
    members m
RIGHT JOIN committees c on c.name = m.name;

>>>
+-----------+--------+--------------+-----------+
| member_id | member | committee_id | committee |
+-----------+--------+--------------+-----------+
|         1 | John   |            1 | John      |
|         3 | Mary   |            2 | Mary      |
|         5 | Amelia |            3 | Amelia    |
|      NULL | NULL   |            4 | Joe       |
+-----------+--------+--------------+-----------+
```

2.uses the right join clause with the `USING` syntax:

```vim
SELECT 
    m.member_id, 
    m.name AS member, 
    c.committee_id, 
    c.name AS committee
FROM
    members m
RIGHT JOIN committees c USING(name);
```

3.find the committee members who are not in the members table:
- use the right join to select data that exists only in the right table:

```vim
SELECT 
    m.member_id, 
    m.name AS member, 
    c.committee_id, 
    c.name AS committee
FROM
    members m
RIGHT JOIN committees c USING(name)
WHERE m.member_id IS NULL;

>>>
+-----------+--------+--------------+-----------+
| member_id | member | committee_id | committee |
+-----------+--------+--------------+-----------+
|      NULL | NULL   |            4 | Joe       |
```

### CROSS JOIN clause

The `cross join` clause does not have a join condition.

The `cross join` makes a Cartesian product of rows from the joined tables. The cross join combines each row from the first table with every row from the right table to make the result set.

i.e. the first table has `n` rows and the second table has `m` rows. The cross join that joins the tables will return `nxm` rows.

**The cross join is useful for generating planning data.** 
- _For example, you can carry the sales planning by using the cross join of customers, products, and years._

**Basic Syntax:**

```vim
SELECT select_list
FROM table_1
CROSS JOIN table_2;
```

**Example:**

Uses the `cross join` clause to join the `members` with the `committees` tables:

```vim
SELECT 
    m.member_id, 
    m.name AS member, 
    c.committee_id, 
    c.name AS committee
FROM
    members m
CROSS JOIN committees c;

>>>
| member_id | member | committee_id | committee |
+-----------+--------+--------------+-----------+
|         1 | John   |            4 | Joe       |
|         1 | John   |            3 | Amelia    |
|         1 | John   |            2 | Mary      |
|         1 | John   |            1 | John      |
|         2 | Jane   |            4 | Joe       |
|         2 | Jane   |            3 | Amelia    |
|         2 | Jane   |            2 | Mary      |
|         2 | Jane   |            1 | John      |
|         3 | Mary   |            4 | Joe       |
|         3 | Mary   |            3 | Amelia    |
|         3 | Mary   |            2 | Mary      |
|         3 | Mary   |            1 | John      |
|         4 | David  |            4 | Joe       |
|         4 | David  |            3 | Amelia    |
|         4 | David  |            2 | Mary      |
|         4 | David  |            1 | John      |
|         5 | Amelia |            4 | Joe       |
|         5 | Amelia |            3 | Amelia    |
|         5 | Amelia |            2 | Mary      |
|         5 | Amelia |            1 | John      |
+-----------+--------+--------------+-----------+
```




