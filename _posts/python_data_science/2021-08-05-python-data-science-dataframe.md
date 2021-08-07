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

#### Sorting in dataframe

**Customised Order:** 对dataframe进行排序 - `columns=[]`

优先对 `year` 进行排序:

```vim
data = {'city': ['shanghai', 'shanghai','shanghai', 'beijing','beijing'],
        'year': [2016, 2017, 2018, 2017, 2018],
        'pop':  [1.5, 1.7, 3.6, 2.4, 2.9]
}

frame2 = DataFrame(data, columns=['year', 'city', 'pop'])
print(frame2)

>>>
   year      city  pop
0  2016  shanghai  1.5
1  2017  shanghai  1.7
2  2018  shanghai  3.6
3  2017   beijing  2.4
4  2018   beijing  2.9
```

**Sort by index**

`dataframe.sort_index(axis=1)`

**Sort by values**

`dataframe.sort_values(by='xyz')`

**Sort by value list**

dataframe.sort_values(by=['aaa','bbb'])


#### Get value from dataframe

Get one-dimensional value from 2-dimensional dataframe 从二维的dataframe中提取一维value:

Two methods:
```vim
data = {'city': ['shanghai', 'shanghai','shanghai', 'beijing','beijing'],
        'year': [2016, 2017, 2018, 2017, 2018],
        'pop':  [1.5, 1.7, 3.6, 2.4, 2.9]
}

frame2 = DataFrame(data, columns=['year', 'city', 'pop'])

# Method 1:
print(frame2['city'])

# Method 2:
print(frame2.city)

>>>
0    shanghai
1    shanghai
2    shanghai
3     beijing
4     beijing
Name: city, dtype: object
```

#### Adding new value to dataframe

1.Adding new value to existing dataframe 

对已有的dataframe新增以及赋予新值:

```vim
data = {'city': ['shanghai', 'shanghai','shanghai', 'beijing','beijing'],
        'year': [2016, 2017, 2018, 2017, 2018],
        'pop':  [1.5, 1.7, 3.6, 2.4, 2.9]
}

frame2 = DataFrame(data, columns=['year', 'city', 'pop'])

frame2['new'] = 100
print(frame2)

>>>
   year      city  pop  new
0  2016  shanghai  1.5  100
1  2017  shanghai  1.7  100
2  2018  shanghai  3.6  100
3  2017   beijing  2.4  100
4  2018   beijing  2.9  100
```

2. Adding new value based on pre-conditions

根据已有列的设定条件来自动新增:
- If `city == beijing`, then add a new value of `TRUE`  in a new column; if not, then return `FALSE`


```vim
data = {'city': ['shanghai', 'shanghai','shanghai', 'beijing','beijing'],
        'year': [2016, 2017, 2018, 2017, 2018],
        'pop':  [1.5, 1.7, 3.6, 2.4, 2.9]
}

frame2 = DataFrame(data, columns=['year', 'city', 'pop'])

# if city == beijing, then add a new value of TRUE  in a new column, if not, then return FALSE

frame2['capital'] = frame2.city == 'beijing'
print (frame2)

>>>
    year      city  pop  new  capital
0  2016  shanghai  1.5  100    False
1  2017  shanghai  1.7  100    False
2  2018  shanghai  3.6  100    False
3  2017   beijing  2.4  100     True
4  2018   beijing  2.9  100     True
```

#### Nested dictionary

`Nesting Dictionary` means putting a `dictionary` inside another `dictionary`.

使用字典的嵌套：字典中包含另一个字典

```vim
data = {'city': ['shanghai', 'shanghai','shanghai', 'beijing','beijing'],
        'year': [2016, 2017, 2018, 2017, 2018],
        'pop':  [1.5, 1.7, 3.6, 2.4, 2.9]
}

pop = {'beijing': {2000:1.5, 2009:2.0},
            'shanghai': {2000:2.0, 2009:3.6}
}

frame3 = DataFrame(pop)
print(frame3)

>>>
        beijing  shanghai
2000      1.5       2.0
2009      2.0       3.6

```

**Reverse columns/rows in input table**

将输出的表格行列转换:

```vim
data = {'city': ['shanghai', 'shanghai','shanghai', 'beijing','beijing'],
        'year': [2016, 2017, 2018, 2017, 2018],
        'pop':  [1.5, 1.7, 3.6, 2.4, 2.9]
}

pop = {'beijing': {2000:1.5, 2009:2.0},
       'shanghai': {2000:2.0, 2009:3.6}
}

frame3 = DataFrame(pop)

print(frame3.T)

>>>
           2000  2009
beijing    1.5   2.0
shanghai   2.0   3.6
```









