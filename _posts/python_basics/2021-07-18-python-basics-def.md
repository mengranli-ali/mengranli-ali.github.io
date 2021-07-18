---
layout: post
title: "Python Basics 1: Class, Object, Variables, Modules, Packages"
subtitle: 'Definition of Class, Object, etc'
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Analysis
---

### Class & Instance

在专业术语上,我们将类别称做类型(`class`),而个体叫做实例(`instance`)。

存活的实例对象都有个 “唯一” 的 ID 值。

可用 type 返回实例所属类型。

如要判断实例是否属于特定类型,须用 isinstance 函数。

```vim
issubclass(Liger, object)
```

事实上,所有类型都有一个共同祖先类型 object,它为所有类型提供原始模版,以及系统 所需的基本操作方式。

区别在于,所有类型对 象都是 type 的实例,这与继承关系无关。

```vim
>>> issubclass(Liger, object)
True

>>> id(int)
4486772160

>>> type(int)
<class 'type'>
```
### Names have no type, but objects do.

在 Python 这类动态语言里,**Name**和**Object**是两个实体。

名字不但有自己的类型,要分配内存,还会介入实际执行过程。甚至可以说,名字才是其动态执行模型的基础。

**名字必须与目标对象关联起来才有意义。**

**赋值操作步骤：**
*   准备好右值目标对象(比如上例中的整数对象 100)。
*   准备好名字(通常是常量,保存在特定列表里。比如 x)。
*   在名字空间(namespace)里为两者建立关联。

_赋值操作仅仅是让名字在名字空间NameSpaces里重新关联,而非修改原对象。
但是一个名字只能引用一个对象。_

An object is allowed to have multiple names,无论是在相同或不同的名字空间里。
```vim
>>> x = 1234

>>> y = x

>>> x is y 
True
```

相等操作符=并不能确定两个名字指向同一对象

这涉及到操作符重载,或许它被设定为比较值是否相等。

```vim
>>> a = 1234
>>> b = 1234

>>> a is b # 指向 同对象。 
False

>>>a==b # 值相等。 
True
```
### Variable 变量

变量多次赋值:

```vim
# 123赋值给a
a = 123
b = a
```

### 模块（Module）、包（Package）、库（Library）、应用（Application）、框架（Framework）

「函数」和「类」组成了「模块」，多个「模块」组成了「包」，多个「包」或者多个「模块」组成了「应用程序」，「应用程序」具有某些特定功能且作为依赖提供给其他项目使用叫作「库」，提供某一领域解决方案的「库」叫框架。










