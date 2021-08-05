---
layout: post
title: "Python Data Science: Dataframe"
subtitle: 'Dataframe, n-dimensional array of pandas'
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Science
  - Dataframe
  - Pandas
---

### Dataframe

`Dataframe` is multiple-dimensional `array` of `Pandas`.

The structure of `dataframe` is a `dictionary`; Then it will print out a table.

创建一个字典的dataframe结构 - 生成dataframe结构的表格table:

```vim
# create a variable called data
# structure of data is dictionary

data = {'city': ['shanghai', 'shanghai','shanghai', 'beijing','beijing'],
        'year': [2016, 2017, 2018, 2017, 2018],
        'pop':  [1.5, 1.7, 3.6, 2.4, 2.9]
}

# get a dataframe structure table

frame = DataFrame(data)
print(frame)

>>>
       city  pop  year
0  shanghai  1.5  2016
1  shanghai  1.7  2017
2  shanghai  3.6  2018
3   beijing  2.4  2017
4   beijing  2.9  2018
```





