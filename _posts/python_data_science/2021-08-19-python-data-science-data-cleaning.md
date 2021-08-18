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



