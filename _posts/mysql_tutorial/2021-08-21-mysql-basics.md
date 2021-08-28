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

When executing the `SELECT` statement with an `ORDER BY` clause, MySQL always evaluates the `ORDER BY` clause after the `FROM` and `SELECT` clauses:

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

Sort the result set by **multiple columns**:

```vim
ORDER BY
   column1,
   column2;
```

Sort the result set by a column **in ascending order** and then by another column **in descending order**:

```vim
ORDER BY
    column1 ASC,
    column2 DESC;
```







