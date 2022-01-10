---
layout: post
title: "Python Data Science: Decision Tree"
subtitle: 'Algorithm in decision tree' 
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Science
  - Data Analysis
  - Data Cleaning
  - Algorithm
---
ddd
### Decision Tree

**Data cleaning** is the process of ensuring that your data is correct, consistent and usable.


#### Principles of Data Cleaning

数据清洗规则总结为以下 4 个关键点，统一起来叫“完全合一”:

- 完整性：单条数据是否存在空值，统计的字段是否完善。
- 全面性：观察某一列的全部数值，比如在 Excel 表中，我们选中一列，可以看到该列的平均值、最大值、最小值。我们可以通过常识来判断该列是否有问题，比如：数据定义、单位标识、数值本身。
- 合法性：数据的类型、内容、大小的合法性。比如数据中存在非 ASCII 字符，性别存在了未知，年龄超过了 150 岁等。
- 唯一性：数据是否存在重复记录，因为数据通常来自不同渠道的汇总，重复的情况是常见的。行数据、列数据都需要是唯一的，比如一个人不能重复记录多次，且一个人的体重也不能在列指标中重复记录多次。

### Using Pandas to clean data

Python 的 Pandas 工具基于 NumPy 的工具，专门为解决数据分析任务而创建。Pandas 纳入了大量库，可以利用这些库高效地进行数据清理工作。

**Three principles:**
- Data Completeness
- Data Comprehension

#### 1.Data Completeness

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
