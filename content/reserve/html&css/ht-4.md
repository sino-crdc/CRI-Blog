+++
title= "HTML笔记-4：HTML链接、头部、CSS"
description = ""
summary = ""
toc = true
authors = [ "zhang"]
tags = ["html","css", "笔记"]
categories = []
series = ["前端"]
date= "2021-05-06"
lastmod = "2021-05-07"
draft = false

+++

HTML笔记-4：链接、头部、CSS
<!--more-->

## 链接

html用标签`a`来设置超文本链接，`href`属性指定了链接的目标（Hypertext Reference的缩写）

```html
<a href="url">链接文本</a>
```

> 链接文本不一定是文本，还可以是图片等其他元素。

### target属性

使用`target`属性，你可以定义被连接的文档在何处显示



### id属性

id属性可以“创建一个**标签**（书签）”，一般用于目录的跳转

演示：

```html
<a id="tips">AAA</a>

<a href="#tips">访问AAA</a>
```



+ 请始终添加**正斜杠**`/`到子文件夹，否则会产生两次请求

  `href="https://www......com/html/`

## HEAD

`<head>` 元素包含了所有的头部标签元素。在 `<head>`元素中你可以插入脚本（scripts）, 样式文件（CSS），及各种meta信息。

可以添加在头部区域的元素标签为: `<title>`, `<style>`, `<meta>`, `<link>`, `<script>`, `<noscript>`和 `<base>`。

