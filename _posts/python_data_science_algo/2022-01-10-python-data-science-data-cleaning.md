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

### Decision Tree

**Decision Tree:** It will go through two stages: Constructing(构造) and Pruning(剪枝).


#### Constructing 构造

构造就是生成一棵完整的决策树。 构造的过程就是选择什么属性作为节点的过程。

在构造过程中，会存在三种节点：
- 根节点：就是树的最顶端，最开始的那个节点。在上图中，“天气”就是一个根节点
- 内部节点：就是树中间的那些节点，比如说“温度”、“湿度”、“刮风”
- 叶节点：就是树最底部的节点，也就是决策结果(RESULT)

**PARENTING:** 节点之间存在父子关系。比如根节点会有子节点，子节点会有子子节点，但是到了叶节点就停止了，**叶节点不存在子节点**。

**While constructing a decision tree, you need to consider:**
- 选择哪个属性作为根节点
- 选择哪些属性作为子节点
- 什么时候停止并得到目标状态，即叶节点

#### Pruning 剪枝

**Pruning:** 剪枝就是给决策树瘦身，这一步想实现的目标就是，不需要太多的判断，同样可以得到不错的结果。这是为了防止“过拟合”（Overfitting）现象。

**Overfitting:** 模型的训练结果“太好了”，以至于在实际应用的过程中，会存在“死板”的情况，导致分类错误。

**Why overfitting happened?** 训练集中样本量较小!
- 如果决策树选择的属性过多，构造出来的决策树一定能够“完美”地把训练集中的样本分类
- 但是这会把训练集中一些数据的特点当成所有数据的特点，但这个特点不一定是全部数据的特点
- 这就使得这个决策树在真实的数据分类中出现错误，也就是模型的“泛化能力”差。

**泛化能力:**
分类器是通过训练集抽象出来的分类能力，即举一反三的能力。
如果我们太依赖于训练集的数据，那么得到的决策树容错率就会比较低，泛化能力差。
因为训练集只是全部数据的抽样，并不能体现全部数据的特点。


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
