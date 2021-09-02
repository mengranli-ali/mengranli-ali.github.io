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



