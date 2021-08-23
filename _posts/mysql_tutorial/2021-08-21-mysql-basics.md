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

[MySQL Tutorial](https://www.mysqltutorial.org/mysql-basics/)

SQL is case-insensitive, you can write the SQL statement in lowercase, uppercase, etc.

Example:

```vim
select select_list
from table_name;
```

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

MySQL doesn’t require the `FROM` clause. It means that you can have a `SELECT` statement without the `FROM` clause 

```vim
SELECT select_list;
SELECT NOW();
SELECT CONCAT('John',' ','Doe');
```

**3.Assign an alias to a column to make it more readable.**

To change a column name of the result set, you can use a column alias:

```vim
SELECT expression AS column_alias;

# or
SELECT expression column_alias;

# for example:
SELECT CONCAT('John',' ','Doe') AS name;
```






