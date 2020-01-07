---
title: Python知识点回顾
date: 2019-04-29 20:43:53
tags:
  - python
categories:
  - python学习笔记
---

<center>刷题中碰到的一些知识点，记录一下</center>

<!-- more -->

# Python知识点回顾

## set()函数

```python
def commonCharacterCount(s1, s2):
    com = [min(s1.count(i),s2.count(i)) for i in set(s1)]
    return sum(com)
```

可通过set(str)直接构造，主要是利用[set()](http://www.runoob.com/python/python-func-set.html)特性解题，无序不重复的元素集，用来判断元素是否重复（多次出现），及计算交集、差集、并集。

## continue & break

continue跳过当前循环，进入下一个循环。

break跳出当前循环，若为多层循环，比如两个for循环嵌套，则跳至上层for循环。

可用来实现[某些题目](https://app.codesignal.com/arcade/intro/level-2/xskq4ZxLyqQMCLshr)中的终止条件。

## zip()函数

待完善

## map()函数

```python
def isLucky(n):
    s = str(n)
    pivot = len(s)//2
    left, right = s[:pivot], s[pivot:]
    return sum(map(int, left)) == sum(map(int, right))
```

求和时使用[map()函数](http://www.runoob.com/python/python-func-map.html)，对列表快速操作求和，可自定义func。sum()函数也可

## list.copy()

完全复制一个列表，复制后两列表操作不会互相影响。

```python
str1 = str2
str1.sort()
print(str2)
```

虽然并未对str2操作，此时输出的str2已为有序，python中使用 ‘=’ 相当于给数组又取了一个名字，正如“刘强东”“东哥”“强子”指的都是奶茶妹妹的老公...而使用 list.copy() 则可以完全复制一个列表，并随意进行操作。

```python
str1 = str2.copy()
```

此时对str1随意操作，就对str2毫无影响了。

## 循环操作

```python
def allLongestStrings(inputArray):
    m = max(len(s) for s in inputArray)
    r = [s for s in inputArray if len(s) == m]
    return r
```

利用循环操作与函数结合，求最大长度并生成包含最长字符串的数组。

## enumerate()函数

```python
def sortByHeight(a):

    l = sorted([i for i in a if i > 0])
    for n,i in enumerate(a):
        if i == -1:
            l.insert(n,i)
    return l
```

[enumerate()函数](http://www.runoob.com/python/python-func-enumerate.html)可同时列出数据和数据下标，可添加参数[start = 0]设置下标起始位置。

此题思路一致，先排序再插入，但是我写的要麻烦一点，写了个单独的循环找坐标，相当于手动实现了enumerate()函数。

## 栈操作

```python
def reverseInParentheses(inputString):

    stack = []
    for item in inputString:
        if item == ')':
            temp = ""
            while stack[-1] != '(':
                temp += stack.pop()
            stack.pop()
            for k in temp:
                stack.append(k)
        else:
            stack.append(item)
    return "".join(stack)
```

借助栈操作来进行逆置，结合判断条件来进行解题。

## 返回条件式

```python
def palindromeRearranging(inputString):

    return sum([inputString.count(i)%2 for i in set(inputString)]) <= 1
```

```python
def areEquallyStrong(yourLeft, yourRight, friendsLeft, friendsRight):
    return {yourLeft, yourRight} == {friendsLeft, friendsRight}
   #return sorted([yourLeft,yourRight])==sorted([friendsLeft,friendsRight])
```

```python
def isIPv4Address(s):
    p = s.split('.')

    return len(p) == 4 and all(n.isdigit() and 0 <= int(n) < 256 for n in p)

```

任何一个逻辑表达式都会返回一个布尔值，构造满足题目要求的条件，如上代码中的 字母单数次数，直接决定字符串是否满足回文的条件。以及判断IP地址是否满足IPv4的条件，结合[all()](http://www.runoob.com/python/python-func-all.html)函数使用。

## sorted()

```python
def avoidObstacles(inputArray):
    c = 2
    while True:
        if sorted([i%c for i in inputArray])[0]>0:
        # if all(x%i!=0 for x in inputArray):
            return c
        c += 1
        
```

[sort 与 sorted 区别：](http://www.runoob.com/python/python-func-sorted.html)

sort 是应用在 list 上的方法，sorted 可以对所有可迭代的对象进行排序操作。

list 的 sort 方法返回的是对已经存在的列表进行操作，无返回值，而内建函数 sorted 方法返回的是一个新的 list，而不是在原来的基础上进行的操作。