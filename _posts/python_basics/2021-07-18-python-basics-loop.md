---
layout: post
title: "Python Basics 2: Array, String, Tup, List, Loop"
subtitle: 'Definition of Array, Loop etc'
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Analysis
---

### Array 序列

Definition:

指它的成员都有序排列，并可以通过下标偏移量访问到它的一个或几个成员.

Array includes 字符串 `String `，列表 `List` ，元组 `Tup`.

先定义一个字符串来保存生肖 - create a variable:

```vim
chinese_zodiac = 'abcdefghijkl'
print(chinese_zodiac[0:4])
print(chinese_zodiac[-1])

>>>abcd
>>>l
```

#### Array 1： `String` 字符串 `‘abcd'`

```vim
chinese_zodiac = '猴鸡狗猪鼠牛虎兔龙蛇马羊'
year1 = 2018
year2 = 1994
print(chinese_zodiac[year1 % 12])
print(chinese_zodiac[year2 % 12])

>>>狗
>>>狗
```

**序列基本操作1： 成员关系操作符**

in array a / not in array a

```vim
print('狗'in chinese_zodiac)
print('狗'not in chinese_zodiac)"

>>>True
>>>False
```
**序列基本操作2： 连接操作符**

array a + array b （两个字符串可以直接相加）

```vim
print(chinese_zodiac + chinese_zodiac)
print(chinese_zodiac + 'abcd')

>>>猴鸡狗猪鼠牛虎兔龙蛇马羊猴鸡狗猪鼠牛虎兔龙蛇马羊
>>>猴鸡狗猪鼠牛虎兔龙蛇马羊abcd
```

**序列基本操作3： 重复操作符**

array a * integer

```vim
print(chinese_zodiac * 3)
```

**序列基本操作4： 切片操作符**

```vim
array [0:integer]
```

#### Array 2: 元组 `Tup` -  `['abc', 'def']`

**使用lambda从序列a中取出小于b的元素**

**_Using lambda to select elements less than b from array a_** 

```vim
a = (1,3,5,7)
b = 4

# 取出a中小于4的元素
print(list(filter(lambda x: x < b, a)))

# 取出a中小于6的元素
b = 6
print(list(filter(lambda x: x < b, a)))

>>>[1, 3]
>>>[1, 3, 5]
```

**使用lambda从序列a中取出小于b的元素的个数**

_**Using lambda to calculate the number of elements less than b selected from array a._**

```vim
a = (1,3,5,7)

# 取出a中小于4的元素的个数
b = 4
print(len(list(filter(lambda x: x < b, a))))

# 取出a中小于6的元素的个数
b = 6
print(len(list(filter(lambda x: x < b, a))))

>>>2
>>>3
```

**如何使用元组来计算日期属于哪个生肖**

_**Using Tup to calculate which date belongs to which Chinese zodiac._**

```vim
zodiac_name = ('mojiezuo', 'shuipingzuo','baiyangzuo','jinniuzuo','shuagnyuzuo')

zodiac_days = ((1,20), (2,18),(3,21),(4,25),(5,21))

(month, day) = (3, 15)

zodiac_day = filter(lambda x:x <=(month, day), zodiac_days)
zodiac_len = len(list(zodiac_day)) % 5
print(zodiac_len)
print(zodiac_name[zodiac_len])

>>>2
>>>baiyangzuo
```

#### Array 3: 列表 `List` - `[0, 'abcd']`

列表跟元组最大区别是可以增删元素

The main difference between `list` and `tup` is: **`list` can add/remove elements**

**Add elements in list a** _**append - 在列表中增加元素**_

```vim
a_list = [0,'abc', 'xyz']
a_list.append('yyy')
print(a_list)

>>>[0, 'abc', 'xyz', 'yyy']
```

**Remove elements from list a** - **_在列表中删除元素_**

```vim
a_list.remove(0)
print(a_list)

>>>['abc', 'xyz', 'yyy']
```







