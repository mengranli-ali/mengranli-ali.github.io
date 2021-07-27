---
layout: post
title: "Python Basics 6: Class & Object-oriented Programming(OOP)"
subtitle: 'Definition of OOP, Class and Instance'
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Analysis
---

### Class and Instance

**Class(类):** A Class is like an object constructor.

A user-defined prototype for an object that defines a set of attributes that characterize any object of the class. The attributes are data members (class variables and instance variables) and methods, accessed via dot notation.

用来描述具有相同的属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法。对象是类的实例。

**Object(对象):** A unique instance of a data structure that's defined by its class. An object comprises both data members (class variables and instance variables) and methods.

- Class variables & Instance variables
- Methods

**Instance(实例):** An individual object of a certain class. An object obj that belongs to a class Circle, for example, is an instance of the class Circle.

**Example:**

面向对象编程: 把相同属性的对象归类

self means 把类实例化后的实例本身

```vim
class Player():  #define a class
    def __init__(self, name, hp):
        self.name = name
        self.hp = hp
    def print_role(self):   #define a method
        print('%s: %s' % (self.name, self.hp))

user1 = Player('tom', 100)  #类的实例化
user2 = Player('jerry', 90)

# call methods from the parent class
user1.print_role()
user2.print_role()

>>>
tom: 100
jerry: 90
```

### Adding attributes/methods to class

**1.Adding class attributes**

增加类的属性

```vim
class Player():
    def __init__(self, name, hp, occu):
        self.name = name  #变量被称作属性
        self.hp = hp
        self.occu = occu
    def print_role(self):
        # output
        print('%s: %s %s' % (self.name, self.hp, self.occu))

class Monster():
    #定义monster class
    pass

#增加更多参数，传递到这个player类中，然后给user1增加属性
user1 = Player('tom', 100, 'war')
user2 = Player('jerry', 90, 'master')
user1.print_role()
user2.print_role()

>>>tom: 100 war
>>>jerry: 90 master
```

**2.Adding class methods**

增加类的方法

```vim
# coding=utf-8

class Player():
    def __init__(self, name, hp, occu):
        self.name = name  #变量被称作属性
        self.hp = hp
        self.occu = occu
    def print_role(self):
        # output
        print('%s: %s %s' % (self.name, self.hp, self.occu))

    # add a new method
    def updatedName(self, newname):
        self.name = newname

class Monster():
    #定义monster class
    pass

#增加更多参数，传递到这个player类中，然后给user1增加属性
user1 = Player('tom', 100, 'war')
user2 = Player('jerry', 90, 'master')
user1.print_role()
user2.print_role()

user1.updatedName('wilson')
user1.print_role()

>>>wilson: 100 war
```

**3.Make sure variables wont be changed**

确保变量不会被实例访问并修改。

这样如果想修改某一个属性，只能通过方法来改变属性，而不能通过赋值来改变。

`self.__name = name`

```vim
class Player():
    def __init__(self, name, hp, occu):
        self.__name = name  #变量被称作属性
        self.hp = hp
        self.occu = occu
    def print_role(self):
        # output
        print('%s: %s %s' % (self.__name, self.hp, self.occu))

    # add a new method
    def updatedName(self, newname):
        self.__name = newname

class Monster():
    #定义monster class
    pass

user1 = Player('tom', 100, 'war')
user1.updatedName('wilson')
user1.print_role()
user1.__name = ('Lily')
user1.print_role()

>>>
tom: 100 war
jerry: 90 master
wilson: 100 war
wilson: 100 war
```

### Class Inheritance 类的继承

普通方法是 `parent_class.__init__(self)`

super方法是 `super(child_class, self).__init__()`

Animal is parent_class of Cat class
Cat is child_class of Animal class

猫继承了猫科动物所使用的方法, 因此猫科动物就是猫的父类, 猫就是猫科动物的子类。





