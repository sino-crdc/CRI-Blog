+++
title= "HTML笔记-1：Web语言"
description = ""
summary = ""
toc = true
authors = [ "zhang"]
tags = ["html","css", "笔记"]
categories = []
series = ["前端"]
date= "2021-04-17"
lastmod = "2021-04-17"
draft = false

+++

HTML笔记-1：Web语言
<!--more-->

# Web语言

## 初识HTML

```html
<html>
    <head>
        <title>Head First Lounge</title>
    </head>
    <body>
        <h1>Welcome!</h1>
        <img src="drink.gif">
        <p>
            html est <em>trop diffcile</em> pour moi
            comme est-ce que tu trouve?
        </p>
        <h2>Directions</h2>
        <p>
            je suis d'accord!
        </p>
    </body>
</html>
```

`<h1>`~`<h6>`标记用来标记标题一到六级

`<p>`用来标记包围一个文本块，称为一个段落

> 不用把匹配的标记放在同一行上

`<html></html>`标记一整个HTML文件

`<head>`用来标记包含页面信息的部分，比如标题`<title>`

`<body>`标记页面主体，包含内容与结构

**元素=开始标记 + 内容 + 结束标记**

## CSS

层叠样式表

### `style`元素

放在`<head>`中

```html
<head>
    <title>coffee</title>
    <style type="text/css">
        
         
    </style>
</head>
```

`style`有一个`type`属性，告诉使用什么样的样式（写不写无所谓）

```html
<head>
    <title>coffee</title>
    <style type="text/css">
        body {            <!--指的是应用到body元素中-->
            background-color: #d2b48c;<!--设置背景色-->
            margin-left: 20%;<!--设置左右边距-->
            margin-right: 20%;
            border: 2px dotted black;<!--定义页面主体周围的边框是虚线，黑色-->
            padding: 10px 10px 10px 10px;<!--在页面主体周围创建一些内边距-->
            font-family: sans-serif;<!--定义文本使用的字体-->
        }
         
    </style>
</head>
```

