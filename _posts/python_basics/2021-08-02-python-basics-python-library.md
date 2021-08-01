---
layout: post
title: "Python Basics 8: Python Library & Regular Expression"
subtitle: 'Use of Python Library & Regular Expression'
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Analysis
---

### Python Library

**library References**

The **[Python Standard Library](https://docs.python.org/3/library/)** 

### Regular Expression 正则表达式库re

#### **1.匹配固定字符**

```vim
import re

# match a fixed string
# p to match with
p = re.compile('a')
# to be matched with
ok = p.match('a')
print(ok)

>>>
<_sre.SRE_Match object at 0x10ab71ed0>
```

#### **2.匹配特殊字符***

```vim
import re

# match a fixed string
# p to match with
p = re.compile('ca*t')
# to be matched with
ok = p.match('caaaaaat')
print(ok)

>>>
<_sre.SRE_Match object at 0x103212100>

```

#### **3.正则表达式的元字符**

全部符合： `.`

```vim
import re

# .
p = re.compile('.')
ok = p.match('caaaaaat')
print(ok)

>>>
<_sre.SRE_Match object at 0x106ffce68>
```

匹配三个字符： `...`

```vim
import re

# ...
p = re.compile('...')
ok = p.match('cccc')
print(ok)

>>>
<_sre.SRE_Match object at 0x1041f4e68>
```

以xxx开头： `^`

```vim
# ...
p = re.compile('^c')
ok = p.match('bccc')
print(ok)

# ...
p = re.compile('^b')
ok = p.match('bccc')
print(ok)

>>>
None

<_sre.SRE_Match object at 0x10494fe68>
```

以xxx结尾 从后边向前边匹配： `$`

```vim
import re

# ...
p = re.compile('jpg$')
ok = p.match('')
print(ok)

>>>

```

`x* `表示*前面的这个字符出现了0次或多次

```vim
import re

# ...
p = re.compile('ca*t')
ok = p.match('caaaat')
print(ok)

import re

# ...
p = re.compile('ca*t')
ok = p.match('ct')
print(ok)

>>>
<_sre.SRE_Match object at 0x10ea99100>

<_sre.SRE_Match object at 0x10caca100>
```

`x+ `表示+前面的这个字符出现了1次或多次

```vim
import re

# ...
p = re.compile('ca+t')
ok = p.match('cat')
print(ok)

import re

# ...
p = re.compile('ca+t')
ok = p.match('ct')
print(ok)

>>>
<_sre.SRE_Match object at 0x105204100>

None
```

`x?` 表示+前面的这个字符出现了0次或1次

```vim
p = re.compile('ca?t')
ok = p.match('ct')        # Appears 0 times

p = re.compile('ca?t')
ok = p.match('caat')    # Appears 2 times

>>>
<_sre.SRE_Match object at 0x101891100>

None
```

`{x}` 前面的字符出现x次

```vim
import re

# ...
p = re.compile('ca{4}t')
ok = p.match('caaat')
print(ok)

p = re.compile('ca{4}t')
ok = p.match('caaaat')

>>>
None

<_sre.SRE_Match object at 0x1031d4100>
```

`{x, y}` 前面的字符出现x到y次

```vim
import re

# ...
p = re.compile('ca{4,6}t')
ok = p.match('caaaaaat')
print(ok)

>>>
<_sre.SRE_Match object at 0x10d322100>
```

`c.t`
- cat
- cbt
- cct

匹配开头和结尾相同的组合，中间字符不同

```vim
import re

# ...
p = re.compile('c.t')
ok = p.match('cbt')
print(ok)

>>>
<_sre.SRE_Match object at 0x10370de68>
```

`c[bcd]t`
- cbt
- cct
- cdt

```vim
import re

# ...
p = re.compile('c[bcd]t')
ok = p.match('cct')
print(ok)

>>>
<_sre.SRE_Match object at 0x10b8ffe68>
```

####  Other Symbols

`\s` 匹配任意空白符

`\d` 匹配单个数字

`\d+` 匹配多个连续数字

`\d{5}` 匹配指定个数(5个)的数字

`\D` 匹配不包含的数字

`()` 小括号
- 2018-03-04提取年月份, 就要分组group
- (2018) - (03) - (04)

`^$` 匹配空行

 `abc*` 贪婪模式：(_不加问号, 就会匹配所有的image_)

_abcccccd_


`.*?` 非贪婪模式匹配不适用贪婪模式:加上问号, 只会匹配到第一个image
```vim
<img   /img>
<img   /img>
```


### Examples of Regular Expression

**正则表达式分组功能实例**

`.{3}` 表示任意一个字符出现3次或3次以上

```vim
import re

# ...
p = re.compile('.{3}')
ok = p.match('cc')
print(ok)

```

`.group()` and `.groups()` 

如何匹配年月份,把年月日取出来:

```vim
# coding=utf-8
import re

# ...
# r表示不要转译 原样输出
p = re.compile(r'(\d+)-(\d+)-(\d+)')
ok = p.match('2018-05-10')

print(ok)

>>>
<re.Match object; span=(0, 10), match='2018-05-10'>
```

Use `.group()`

```vim
# coding=utf-8
import re

# ...
# r表示不要转译 原样输出
p = re.compile(r'(\d+)-(\d+)-(\d+)')
ok = p.match('2018-05-10')

year = ok.group(1)
month = ok.group(2)
day = ok.group(3)
date = ok.group(0)   # = ok.group()

print(year)
print(month)
print(day)
print(date)

>>>
2018
05
10
2018-05-10
<_sre.SRE_Match object at 0x1102d0f08>
```

```vim
# coding=utf-8
import re

# ...
# r表示不要转译 原样输出
p = re.compile(r'(\d+)-(\d+)-(\d+)')
d = ('2020-11-11')
ok = p.match(d)

year = ok.group(1)
month = ok.group(2)
day = ok.group(3)
date = ok.group(0)   # = ok.group()

print(year)
print(month)
print(date)

>>>
2020
11
2020-11-11
```

use `.groups()`

```vim
# coding=utf-8
import re

# ...
# r表示不要转译 原样输出
p = re.compile(r'(\d+)-(\d+)-(\d+)')
ok = p.match('2018-05-10')
year, month, date = ok.groups()
print(year)
print(month)
print(date)
print(ok)

>>>
2018
05
10
<_sre.SRE_Match object at 0x107157e70>
```

### Difference between `.match()` and `.search()`

**正则表达式库函数match与search的区别:**

`.search()`可以匹配字符串中的日期, 无须fully matched

`.match()` 必须从**字符串开头**进行匹配，相当于自带了一个 ^

```vim
# coding=utf-8
import re

# ...
# r表示不要转译 原样输出
p = re.compile(r'(\d+)-(\d+)-(\d+)')
d = ('2020-11-11bb')
ok = p.search(d)
ok1 = p.match(d)
ok2 = p.match('aa2020-11-11bb')

print(ok)
print(ok1)
print(ok2)

>>>
<re.Match object; span=(0, 10), match='2020-11-11'>
<re.Match object; span=(0, 10), match='2020-11-11'>
None
```

### How to use .sub()

**正则表达式库替换函数sub()的实例:**

`.sub()` 用于字符串的替换

Example 1: 把phone字符串里面的#后面部分替换为空白
- use `r` to escape character;`r` 是声明这个字符串里面是正则表达式的元字符
- `r'#.*$'` to replace the `#`symbol until the end `$`

```vim
# coding=utf-8
import re

phone = '123-456-789 # this is phone number'
# `r'#.*$'` to replace the #symbol until the end$
# use r to escape character
# in the middle ' ' means sth to place with
p2 = re.sub(r'#.*$', ' ', phone)
print(p2)

>>>
123-456-789 
```

Example 2: 把phone字符串里面的 `-` 替换掉

使用 `r'\D' `把所有非数字的字符替换掉 - Replace all non-number symbols

```vim
# coding=utf-8
import re

phone = '123-456-789 # this is phone number'
p1 = re.sub(r'#.*$', '', phone)
p2 = re.sub(r'\D', '', p1)
print(p2)

>>>
123456789
```

### How to use `.findall()`

`.findall()` 是找到所有匹配的字符串

`.findall()`、`.match()`、`.sub()`、`.search()`分别是不同的函数功能，并非是扩展，例如.search()函数是找到第一个匹配的字符串.

Example: Find all numbers in string and return string '123'
```vim
import re

string = "x abc y 123 z 123"
pattern = re.compile(r'\d+')

print(re.search(pattern,string))
print(pattern.findall(string))

>>>
<re.Match object; span=(8, 11), match='123'>
['123', '123']
```


## time and datetime 日期与时间函数库

`time.localtime()` 当地时间

```vim
import time

print(time.time())
print(time.localtime())

>>>
1616618004.89
time.struct_time(tm_year=2021, tm_mon=3, tm_mday=24, tm_hour=20, tm_min=33, tm_sec=24, tm_wday=2, tm_yday=83, tm_isdst=0)
```

`time.strftime()` 

1.输入年月日

```vim
import time

print(time.strftime('%Y-%m-%d'))

>>>
2021-08-01

```

2.输入时分秒

```vim
print(time.strftime('%Y-%m-%d %H:%M:%S'))

>>>
2021-08-01 20:43:52
```

3.输出年月日没有空格

```vim
print(time.strftime('%Y%m%d'))

>>>
20210801
```

4.输出现在的时间

```vim
import datetime

print(datetime.datetime.now())

>>>
2021-08-01 20:46:20
```

5.输出当前时间的十分钟后的时间

```vim
import datetime

print(datetime.datetime.now())
newtime = datetime.timedelta(minutes=10)
print(datetime.datetime.now() + newtime)

>>>
2021-03-24 20:48:20.721565
2021-03-24 20:58:20.721612
```

6.输出某一天的基础上再加10天

```vim
import datetime
one_day = datetime.datetime(2020,1,20)
new_date = datetime.timedelta(days=10)
print(one_day + new_date)

>>>
2020-01-30 00:00:00
```

## Math-related 数学相关库

1.`.math()` - Mathematical Functions

用于ML DL，计算正弦值余弦值

2.`.random()` - Generate pseudo-random numbers

用于软件测试有限定条件的随机数

`random.randint()`

Example: 输出一个1-5之间的随机整数值

```vim
import random
a = random.randint(1,5)

print(a)
```

`random.choice([])`

Example: 输出一个aa-cc的随机字符串

```vim
import random

b = random.choice(['aa', 'bb', 'cc'])
print(b)
```

