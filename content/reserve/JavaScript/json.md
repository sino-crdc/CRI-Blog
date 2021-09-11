+++
title= "json格式详解"
description = ""
summary = ""
toc = false
authors = [ "zhang"]
tags = ["json","javascript", "笔记"]
categories = []
series = ["前端"]
date= "2021-05-20"
lastmod = "2021-05-21"
draft = false

+++

<!--more-->

json： enmmm[ ][^2]

一种数据表示格式

> **JSON**（**J**ava**S**cript **O**bject **N**otation，JavaScript对象表示法，读作/ˈdʒeɪsən/）是一种由道格拉斯·克罗克福特构想和设计、轻量级的资料交换语言，该语言以易于让人阅读的文字为基础，用来传输由属性值或者序列性的值组成的数据对象。尽管JSON是JavaScript的一个子集，但JSON是独立于语言的文本格式，并且采用了类似于C语言家族的一些习惯。——[维基百科][^1]

## json构建于两种结构

1. “名称/键值对”的集合（**无序**）
2. 值的**有序**列表

### 1. 对象（object）

形式：大括号

```json
{string1:value1, string2:value2,...}
```

### 2.数组（array）

形式：方括号

```json
[value1, value2,...]
```

+ 这些形式都是可以嵌套的

  `value` 可以是`string`、`number`、`true`、`false`、`object`、`array`等

+ `string` 是用双引号包围的任意数量的Unicode字符的集合

+ 对象的每个属性都要有<font color=red size=3>双引号</font>，否则不能正常加载

+ 嵌套参考：

  ```json
  [
       {
            "text": "This is the text",
            "color": "dark_red",
            "bold": "true",
            "strikethough": "true",
            "clickEvent":
                 {
                      "action": "open_url",
                      "value": "zh.wikipedia.org"
                 },
            "hoverEvent":
                 {
                      "action": "show_text",
                      "value":
                      {
                           "extra": "something"
                      }
                 }
       },
       {
            "translate": "item.dirt.name",
            "color": "blue",
            "italic": "true"
       }
  ]
  ```

  

参考资料：

[^1]:https://zh.wikipedia.org/wiki/JSON
[^2]:http://www.json.org/json-zh.html

