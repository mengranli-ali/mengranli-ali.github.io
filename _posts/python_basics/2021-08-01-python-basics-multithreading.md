---
layout: post
title: "Python Basics 7: Concurrency & Multithreading"
subtitle: 'Definition of Multithreading'
author: "Mengran"
header-style: text
tags:
  - Python
  - Data Analysis
---

### Multithreading

Scenario: There is a long queue for supermarket but only one till is running.

超市只有一个收银台但是排很长队 就需要multitasking

**Normal `for` loop - only one thread**

```vim
def myThread(arg1, arg2):
    print('%s %s' % (arg1, arg2))

# loop from 1,6
# everytime increment 1

for i in range(1,6,1):
    #调用myThread函数
    t1 = myThread(i, i+1)

>>>
1 2
2 3
3 4
4 5
5 6
```

**Use multiple threads**

使用多线程方法: 由于是多线程程序，输出内容不按顺序显示是正常现象
- import threading 引入多线程包


```vim
# coding=utf-8
import threading
from threading import current_thread
import time


def myThread(arg1, arg2):
    print(current_thread().getName(), 'start')
    print('%s %s' % (arg1, arg2))
    print(current_thread().getName(), 'stop')


# loop from 1,6
# everytime increment 1
for i in range(1, 6, 1):
    # 调用myThread函数
    # t1 = myThread(i, i+1)
    # 循环5次 输出5个线程
    t1 = threading.Thread(target=myThread, args=(i, i + 1))
    t1.start()

print(current_thread().getName(), 'end')

>>>
('Thread-1', 'start')
1 2
(('Thread-2', 'Th'rsetaadr(-t1'', 's)top'('Thre)ad-4'

', Th2 3read-3', 'st
ar'ts'tart'('Thread-2', 'stop')
)
4 5
('Thr)ead-4', 'st
op'3 4
('Thre)ad-3'('Th, re(ad
-5''s'tMoapi'nT)hre
ad', 'st, art''e)nd'
)
5 6
('Thread-5', 'stop')
```

### current thread

线程之间的同步: 
- join() method
- 子线程先结束 主线程后结束

```vim
import threading
from threading import current_thread


# 1.define a class
class MyThread(threading.Thread):
    def run(self):
        print(current_thread().getName(), 'start')
        print('run')
        print(current_thread().getName(), 'stop')


# 2.initiate the class
t1 = MyThread()
t1.start()
# 3. child thread ended first, parent thread ended later
t1.join()

print(current_thread().getName(), 'end')

>>>
# without the join()
(('Ma'iTnhTrheraeda-d1'', , 'en'ds'ta)rt'
)
run
('Thread-1', 'stop')


# with the join()
('Thread-1', 'start')
run
('Thread-1', 'stop')
('MainThread', 'end')
```

### 经典的生产者和消费者问题

当生产速度大于消费速度，且队列已经满了时，将不再生产。当消费速度大于生产速度，且没有消费的对象后，则消费者不再消费。

**1.队列 Queue**

```vim
import queue
q = queue.Queue()
q.put(1)
q.put(2)
q.put(3)


```

**2.Adding elements to the queue**

在队列里增加数据:

```vim


q.get()
q.get()

>>>
1
2
```

**3. Multiple threading**

```vim
# coding=utf-8
# 实现多个消费者和生产者并行的线程

from threading import Thread, current_thread
import time
import random
import Queue

# set the length of queue to 5
queue = Queue.Queue(5)


class ProducerThread(Thread):
    def run(self):
        # first to get name of the thread
        name = current_thread().getName()
        nums = range(100)
        global queue
        while True:
            # then select a random number
            num = random.choice(nums)
            # then put the number into the queue
            queue.put(num)
            print('Producer %s produces %s data' % (name, num))
            # based on random time, to add numbers to queue
            t = random.randint(1, 3)
            time.sleep(1)
            print('Producer %s sleeps %s seconds' % (name, t))


class ConsumerThread(Thread):
    def run(self):
        name = current_thread().getName()
        global queue
        while True:
            # get numbers from the queue
            num = queue.get()
            # task_done() method 封装好了线程等待和同步的代码
            queue.task_done()
            print('Consumer %s consumes %s data' % (name, num))
            t = random.randint(1, 5)
            time.sleep(t)
            print('Consumer %s sleeps %s data' % (name, t))


p1 = ProducerThread(name='p1')
p1.start()
c1 = ConsumerThread(name='c1')
c1.start()
c2 = ConsumerThread(name='c2')
c2.start()

>>>
Producer p1 produces 17 data
Consumer c1 consumes 17 data
Producer p1 sleeps 2 seconds
Producer p1 produces 84 data
Consumer c2 consumes 84 data
Producer p1 sleeps 2 seconds
Producer p1 produces 35 data
Consumer c1 sleeps 3 data
Consumer c1 consumes 35 data
Producer p1 sleeps 2 seconds
Producer p1 produces 0 data
Consumer c2 sleeps 3 data
Consumer c2 consumes 0 data
```


