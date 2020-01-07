---
title: BeautifulSoup学习笔记
date: 2017-09-20 19:47:19
tags:
  - 爬虫
  - 网页解析
  - python
  - BeautifulSoup
categories:
  - python学习笔记
---

<center>BeautifulSoup学习笔记</center>

<!-- more -->

# 支持各种解析器
`BeautifulSoup(markup, "html.parser")`
`BeautifulSoup(markup, "lxml")`

`BeautifulSoup(markup, ["lxml", "xml"])`
`BeautifulSoup(markup, "xml")`

`BeautifulSoup(markup, "html5lib")`

支持几种主要的解析器，包括标准库、HTML解析、XML解析及html5lib等，不同的解析器差别在于执行速度、容错能力以及是否依赖外部库。

# 如何使用
```
from bs4 import BeautifulSoup

soup = BeautifulSoup(open("index.html"))

soup = BeautifulSoup("<html>data</html>")
```
采用Unicode编码，如不指定解析器则BS会选择最合适的解析器来解析文档。

# 对象的种类
>Beautiful Soup将复杂HTML文档转换成一个复杂的树形结构,每个节点都是Python对象,所有对象可以归纳为4种: **Tag** , **NavigableString** , **BeautifulSoup** , **Comment** .

## Tag
包括*Name*和*Attributes*
![Tag](http://owks2feqx.bkt.clouddn.com/Tag.png)

>每个tag都有自己的名字
>`tag.name`

>一个tag可以有很多个属性（所以是Attribute *s*）,其中*类（class）* 可以是多值属性

如图中所示，则
```
tag.attrs
# {u'class': u'boldest'}
或
tag['class']
# u'boldest'
```
## 可遍历字符串
NavigableString 类来包装tag中的字符串
```
tag.string
# u'Extremely bold'
type(tag.string)
# <class 'bs4.element.NavigableString'>
```
## BeautifulSoup
表示一个文档的全部内容,可当做tag对象。

## 注释及特殊字符串
特殊格式，暂不考虑

# 遍历文档树
![soup操作](http://owks2feqx.bkt.clouddn.com/soup%E6%93%8D%E4%BD%9C.png)

有针对子节点、父节点、兄弟节点、以及查询中前进和后退的相关操作，更多操作查看官方文档。

# 搜索文档树
主要应用find()和find_all(), 方法有：
-   字符串`soup.find_all('b')`
-   正则表达式  `soup.find_all(re.compile("^b"))`
-   列表 `soup.find_all(["a", "b"])`
-   True(匹配所有tag，不返回字符串节点) `soup.find_all(True)`


>针对爬虫的话，上面的内容对文档的解析和搜索已经够用了，后面还有修改文档树等内容，等在实际应用中用到了，继续更新到这里。

>此次整理的内容没有太多实践的辅助，主要是跟着官方文档里面的例子应用了下函数，看了下输出结果，内容多是官方文档的提炼，有待丰富。

>官方文档地址:
[BeautifulSoup 4.2.0文档][b37c96f2]

[b37c96f2]: https://www.crummy.com/software/BeautifulSoup/bs4/doc/index.zh.html# "官方文档"
