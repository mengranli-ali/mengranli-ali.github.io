---
layout: post
title: "Data Analysis: MySQL Basics"
subtitle: 'To Lean basic MySQL statements'
author: "Mengran"
header-style: text
tags:
  - Data Analysis
  - MySQL
---

### MySQL Basics

More details can be found here:

[MySQL Tutorial](https://www.mysqltutorial.org/mysql-basics/)

SQL is case-insensitive, you can write the SQL statement in lowercase, uppercase, etc.

Example:

```vim
select select_list
from table_name;
```

Or:

```vim
SELECT select_list
FROM table_name;
```

#### Querying Data

**1.`SELECT FROM` – query the data from a single table.**

```vim
SELECT select_list
FROM table_name;
```

To query data from multiple columns:

```vim
SELECT 
    lastName, 
    firstName, 
    jobTitle
FROM
    employees;
```

To retrieve data from all columns:
- Use the asterisk (*) which is the shorthand for all columns

```vim
SELECT * 
FROM employees;
```


**2.`SELECT` – to use the SELECT statement without referencing a table.**

MySQL does not require the `FROM` clause. It means that you can have a `SELECT` statement without the `FROM` clause 

```vim
SELECT select_list;
SELECT NOW();
SELECT CONCAT('John',' ','Doe');
```

**3.Assign an alias to a column to make it more readable.**

To change a column name of the result set, you can use a column **alias**:

```vim
SELECT expression AS column_alias;

# or
SELECT expression column_alias;

# for example:
SELECT CONCAT('John',' ','Doe') AS name;
```

#### Sorting Data

To **sort the rows** in the result set, you add the `ORDER BY` clause to the `SELECT` statement.

1.When executing the `SELECT` statement with an `ORDER BY` clause, MySQL always evaluates the `ORDER BY` clause after the `FROM` and `SELECT` clauses:

```vim
SELECT 
   select_list
FROM 
   table_name
ORDER BY 
   column1 [ASC|DESC], 
   column2 [ASC|DESC],
   ...;
```

By default, the `ORDER BY` clause uses `ASC` if you don’t explicitly specify any option. 

Use `ASC` to sort the result set in ascending order:

```vim
ORDER BY column1 ASC;
```

Use `DESC` to sort the result set in descending order:

```vim
ORDER BY column1 DESC;
```

**2.Sort the result set by **multiple columns**:**

```vim
ORDER BY
   column1,
   column2;
```

**3.Sort the result set by a column **in ascending order** and then by another column **in descending order**:**

```vim
ORDER BY
    column1 ASC,
    column2 DESC;
```

**4.Using `ORDER BY` clause to sort a result set by an expression:**

```vim
SELECT orderNumber,
       orderlinenumber,
	   quantityOrdered,
	   priceEach,
	   quantityOrdered * priceEach as totalPrice
FROM orderdetails
ORDER BY totalPrice;

>>>
orderNumber	orderlinenumber	quantityOrdered	priceEach	totalPrice
10419	                 7	          15	32.10	        481.50
10420	                 3	          15	35.29	        529.35
10322	                 3	          20	26.55	        531.00
10407	                 3	           6	91.11	        546.66
```

**5.Using `ORDER BY` clause to sort data using a custom list**

The `FIELD()` function returns the **position of the str** in the str1, str2, … list. 

If the str is not in the list, the `FIELD()` function returns 0. 

For example, the following query returns 1 because the position of the string ‘A’ is the first position on the list 'A', 'B', and 'C':

```vim
FIELD(str, str1, str2, ...)

SELECT FIELD('A', 'A', 'B','C');
```

Example:

Suppose that you want to sort the sales orders based on their statuses in the following order:
- In Process
- On Hold
- Canceled
- Resolved
- Disputed
- Shipped

you can use the `FIELD()` function to **map each order status** to a number and sort the result by the result of the `FIELD()` function:

```vim
SELECT 
    orderNumber, status
FROM
    orders
ORDER BY FIELD(status,
        'In Process',
        'On Hold',
        'Cancelled',
        'Resolved',
        'Disputed',
        'Shipped');
        
>>>
orderNumber	status
10420	In Process
10425	In Process
10334	On Hold
10401	On Hold
10167	Cancelled
10179	Cancelled
10248	Cancelled
10253	Cancelled
10260	Cancelled
10262	Cancelled
10164	Resolved
10327	Resolved
10367	Resolved
10386	Resolved
10406	Disputed
10415	Disputed
10417	Disputed
10100	Shipped
10101	Shipped
```

**6.MySQL `ORDER BY` and `NULL`**

In MySQL, `NULL` comes before `non-NULL `values. 

Therefore, when you the `ORDER BY` clause with the `ASC` option, `NULLs` appear first in the result set.

If you use the `ORDER BY` with the `DESC` option, `NULLs` will appear last in the result set

```vim
SELECT 
    firstName, lastName, reportsTo
FROM
    employees
ORDER BY reportsTo DESC;

>>>
firstName | lastName  | reportsTo |
+-----------+-----------+-----------+
| Yoshimi   | Kato      |      1621 |
| Leslie    | Jennings  |      1143 |
| Leslie    | Thompson  |      1143 |
| Julie     | Firrelli  |      1143 |
| ....
| Mami      | Nishi     |      1056 |
| Mary      | Patterson |      1002 |
| Jeff      | Firrelli  |      1002 |
| Diane     | Murphy    |      NULL 
```

#### Filtering Data

**Basic Operators:**
- `WHERE` – learn how to use the `WHERE` clause to filter rows based on specified conditions.
- `SELECT  DISTINCT` – show you how to use the `DISTINCT` operator in the SELECT statement to eliminate duplicate rows in a result set.
- `AND` – introduce you to the `AND` operator to combine Boolean expressions to form a complex condition for filtering data.
- `OR`– introduce you to the `OR` operator and show you how to combine the OR operator with the AND operator to filter data.
- `IN` – show you how to use the `IN` operator in the WHERE clause to determine if a value matches any value in a set.
- `NOT IN` – negate the `IN` operator using the `NOT` operator to check if a value doesn’t match any value in a set.
- `BETWEEN` – show you how to query data based on a range using `BETWEEN` operator.
- `LIKE`  – provide you with technique to query data based on a pattern.
- `LIMIT` – use `LIMIT` to constrain the number of rows returned by `SELECT` statement
- `IS NULL` – test whether a value is `NULL` or not by using `IS NULL` operator.

**`WHERE` clause**

The `WHERE` clause allows you to specify a search condition for the rows returned by a query. 

The `search_condition` is a combination of one or more expressions using the logical operator `AND`, `OR` and `NOT`.
- `WHERE jobtitle = 'Sales Rep';`
- `WHERE jobtitle = 'Sales Rep' AND officeCode = 1;`
- `WHERE jobtitle = 'Sales Rep' OR officeCode = 1;`
- `WHERE officeCode BETWEEN 1 AND 3`

```vim
SELECT 
    select_list
FROM
    table_name
WHERE
    search_condition;
```

**1.Using `WHERE` clause with equality operator**

```vim
SELECT 
    lastname, 
    firstname, 
    jobtitle
FROM
    employees
WHERE
    jobtitle = 'Sales Rep';
    
>>>
lastname  | firstname | jobtitle  |
+-----------+-----------+-----------+
| Jennings  | Leslie    | Sales Rep |
| Thompson  | Leslie    | Sales Rep |
| Firrelli  | Julie     | Sales Rep |
| Patterson | Steve     | Sales Rep |
| Tseng     | Foon Yue  | Sales Rep |
```

**2.Using `WHERE` clause with the `AND` operator**

```vim
SELECT 
    lastname, 
    firstname, 
    jobtitle,
    officeCode
FROM
    employees
WHERE
    jobtitle = 'Sales Rep' AND 
    officeCode = 1;
    
>>>
lastname | firstname | jobtitle  | officeCode |
+----------+-----------+-----------+------------+
| Jennings | Leslie    | Sales Rep | 1          |
| Thompson | Leslie    | Sales Rep | 1          
```

**3.Using `WHERE` clause with `OR` operator**

The `OR` operator evaluates to `TRUE` only if one of the expressions evaluates to `TRUE`:

The query returns any employee who has the job title Sales Rep or office code 1.

```vim
SELECT 
    lastName, 
    firstName, 
    jobTitle, 
    officeCode
FROM
    employees
WHERE
    jobtitle = 'Sales Rep' OR 
    officeCode = 1
ORDER BY 
    officeCode, 
    jobTitle;
    
>>>
lastName  | firstName | jobTitle           | officeCode |
+-----------+-----------+--------------------+------------+
| Murphy    | Diane     | President          | 1          |
| Bow       | Anthony   | Sales Manager (NA) | 1          |
| Jennings  | Leslie    | Sales Rep          | 1          |
| Thompson  | Leslie    | Sales Rep          | 1          |
| Firrelli  | Jeff      | VP Marketing       | 1          |
| Patterson | Mary      | VP Sales           | 1          |
| Firrelli  | Julie     | Sales Rep          | 2          |
| Patterson | Steve     | Sales Rep          | 2          |
| Tseng     | Foon Yue  | Sales Rep          | 3          |  
```

**4.Using `WHERE` clause with the `BETWEEN` operator** 

The `BETWEEN` operator returns `TRUE` if a value is in a range of values:

`expression BETWEEN low AND high`

```vim
SELECT 
    firstName, 
    lastName, 
    officeCode
FROM
    employees
WHERE
    officeCode BETWEEN 1 AND 3
ORDER BY officeCode;

>>>
firstName | lastName  | officeCode |
+-----------+-----------+------------+
| Diane     | Murphy    | 1          |
| Mary      | Patterson | 1          |
| Jeff      | Firrelli  | 1          |
| Anthony   | Bow       | 1          |
| Leslie    | Jennings  | 1          |
| Leslie    | Thompson  | 1          |
| Julie     | Firrelli  | 2          |
| Steve     | Patterson | 2          |
| Foon Yue  | Tseng     | 3          |
| George    | Vanauf    | 3          |
+-----------+-----------+------------+
```

**5.Using `WHERE` clause with the `LIKE` operator**

The `LIKE` operator evaluates to `TRUE` if a value matches a specified pattern.

To form a pattern, you use the `%` and `_` wildcards(replacements/placeholders):
- The `%` wildcard matches any string of zero or more characters
- The `_` wildcard matches any single character

The following query finds the employees whose last names end with the string 'son':

```vim
SELECT 
    firstName, 
    lastName
FROM
    employees
WHERE
    lastName LIKE '%son'
ORDER BY firstName;

>>>
+-----------+-----------+
| firstName | lastName  |
+-----------+-----------+
| Leslie    | Thompson  |
| Mary      | Patterson |
| Steve     | Patterson |
| William   | Patterson |
+-----------+-----------+
```



