---
layout: post
title: "Python Data Science: Data Cleaning"
subtitle: 'Key principles of data cleaning' 
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Science
  - Data Analysis
  - Data Cleaning
---

### Data Cleaning

**Data cleaning** is the process of ensuring that your data is correct, consistent and usable.


#### Principles of Data Cleaning

数据清洗规则总结为以下 4 个关键点，统一起来叫“完全合一”:

- 完整性：单条数据是否存在空值，统计的字段是否完善。
- 全面性：观察某一列的全部数值，比如在 Excel 表中，我们选中一列，可以看到该列的平均值、最大值、最小值。我们可以通过常识来判断该列是否有问题，比如：数据定义、单位标识、数值本身。
- 合法性：数据的类型、内容、大小的合法性。比如数据中存在非 ASCII 字符，性别存在了未知，年龄超过了 150 岁等。
- 唯一性：数据是否存在重复记录，因为数据通常来自不同渠道的汇总，重复的情况是常见的。行数据、列数据都需要是唯一的，比如一个人不能重复记录多次，且一个人的体重也不能在列指标中重复记录多次。

#### Using Pandas to clean data

Python 的 Pandas 工具基于 NumPy 的工具，专门为解决数据分析任务而创建。Pandas 纳入了大量库，可以利用这些库高效地进行数据清理工作。

**Data Completeness**

Data Completeness includes cleaning missing values and NaN.

**1.Missing Data 缺失值**

在数据中有些年龄、体重数值是缺失的，这往往是因为数据量较大，在过程中，有些数值没有采集到。通常我们可以采用以下三种方法：
- Delete 删除：删除数据缺失的记录；
- Average 均值：使用当前列的均值；
- Use highest frequency data 高频：使用当前列出现频率最高的数据。

**Example 1: Fill missing data in `column['Age'] ` with its average age.**

if you want it to modify the df inplace, you have to explicitly specify

`inplace=True`

`df['age'].fillna(df['age'].mean(), inplace=True)`

```vim
import pandas as pd
from pandas import DataFrame
import numpy as np

df = DataFrame({'name':['ZhangFei', 'GuanYu', 'a', 'b', 'c'], 'age': [23, 19, np.nan, 25, 44]})

df['age'].fillna(df['age'].mean(), inplace=True)

print(df)

>>>
       name    age
0  ZhangFei  23.00
1    GuanYu  19.00
2         a  27.75
3         b  25.00
4         c  44.00
```

**Example 2: Fill missing data with highly frequent value**

如果我们用最高频的数据进行填充，可以先通过 `value_counts` 获取 Age 字段最高频次 `age_maxf`，然后再对 Age 字段中缺失的数据用 `age_maxf` 进行填充:

`age_maxf = df['age'].value_counts().index[0]`

`df['age'].fillna(age_maxf, inplace=True)`

```vim
import numpy as np
import pandas as pd
from pandas import DataFrame
``
df = DataFrame({'name':['ZhangFei', 'GuanYu', 'a', 'b', 'c'], 'age': [23, 25, np.nan, 25, 44]})

age_maxf = df['age'].value_counts().index[0]
df['age'].fillna(age_maxf, inplace=True)

print(df)

>>>
       name   age
0  ZhangFei  23.0
1    GuanYu  25.0
2         a  25.0
3         b  25.0
4         c  44.0
```

**2.Empty rows 空行**

我们发现数据中有一个空行，除了 `index` 之外，全部的值都是 `NaN`。

`Pandas` 的 `read_csv()` 并没有可选参数来忽略空行，这样，我们就需要在数据被读入之后再使用 `dropna()` 进行处理，删除空行。

**Drop the rows where all elements are missing:**

`df.dropna(how='all',inplace=True) `



