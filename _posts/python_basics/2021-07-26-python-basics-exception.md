---
layout: post
title: "Python Basics 4: Exception & Error"
subtitle: 'How to handle Exception and Error'
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Analysis
---

### Exception & Error

Key points:
- Error is not equal to Exception
- Exception 异常 是在出现错误时采用正常控制流以外的动作

How to handle Exception:
1. Detected error, thus triggering exception 检测到错误，引发异常
2. Catch the exception 对异常进行捕获的操作

Syntax:
```vim
try:
   detecting exception
except Exception[, reason]:
   catch exception code
finally:
   implement code no matter if got exception
```


### Types of Exception

#### SyntaxError

语法错误

#### NameError

variable命名错误

#### IndexError

string index out of range

```vim
a = '123'
print(a[3])
```

#### KeyError

IndexError: string index out of range

```vim

d = {'a':1, 'b':2}
print(d['c'])"
```

#### ValueError

ValueError - wrong value

```vim
try:
    year = int(input(""please input here:""))
except ValueError:
    print('You need to input numbers!')

>>>please input here:""asdf"
>>>You need to input numbers!
```

#### AttributeError

AttributeError: 'int' object has no attribute 'append'
```vim
a = 123
a.append()
```

#### ZeroDivisionError

```vim
try:
    print(1/0)
except ZeroDivisionError:
    print('you cant use 0 to divide 1')

```

### How to catch exception

**1.Print error message when catching exception**

捕获错误时也打印出错误信息

Example 1: You can't use 0 to divide 1 integer division or modulo by zero

```vim
try:
    print(1/0)
except ZeroDivisionError as e:
    print('you cant use 0 to divide 1 %s' %e)
```

Example 2: Please input here:"asdf"


```vim
try:
    year = int(input(""please input here:""))
except ValueError as e:
    print('You need to input numbers! %s' %e)
>>>You need to input numbers! invalid literal for int() with base 10: 'asdf'
```

**2.Catch ALL exception and print error message**


```vim
try:
    year = int(input(""please input here:""))
except Exception as e:
    print('You need to input numbers! %s' %e)

>>>please input here:"asdf"
>>>You need to input numbers! invalid literal for int() with base 10: 'asdf'
```


**3.Create your own exception message**

```vim
try:
    raise NameError('helloError')
except NameError:
    print('my custom error')

>>>my custom error
```

### `finally`

`finally` - 无论产生异常与否 都会执行

```vim
try:
    a = open('name1.txt')
except Exception as e:
    print(e)
finally:
    a.close()

>>>NameError: name 'a' is not defined
```

