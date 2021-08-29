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

### Joining Tables

**Basic statements of Joining Tables:**
- `Table & Column Aliases` – introduce you to table and column aliases.
- `Joins`  – give you an overview of joins supported in MySQL including inner join, left join, and right join.
- `INNER JOIN` – query rows from a table that has matching rows in another table.
- `LEFT JOIN` – return all rows from the left table and matching rows from the right table or null if no matching rows found in the right table.
- `RIGHT JOIN` – return all rows from the right table and matching rows from the left table or null if no matching rows found in the left table.
- `CROSS JOIN` – make a Cartesian product of rows from multiple tables.
- `Self-join` – join a table to itself using table alias and connect rows within the same table using inner join and left join.

### MySQL alias for columns

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

### MySQL join clauses

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

### MySQL INNER JOIN clause

Basic syntax of the `inner join` clause that **joins two tables** `table_1` and `table_2`:

```vim
SELECT column_list
FROM table_1
INNER JOIN table_2 ON join_condition;
```

Uses an `inner join` clause to find members who are also the committee members:
- use the values in the name columns in both tables `members` and `committees` to match.

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

### MySQL LEFT JOIN clause

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

### MySQL RIGHT JOIN clause

The `right join` clause is similar to the left join clause except that the treatment of left and right tables is reversed. The right join starts selecting data from the right table instead of the left table.

The `right join` clause selects all rows from the right table and matches rows in the left table. If a row from the right table does not have matching rows from the left table, the column of the left table will have `NULL` in the final result set.

