+++
title= "css笔记-1：选择器"
description = ""
summary = ""
toc = false
authors = [ "zhang"]
tags = ["html","css", "笔记"]
categories = []
series = ["前端"]
date= "2021-04-20"
lastmod = "2021-04-21"
draft = false

+++

css笔记-1：选择器
<!--more-->

# css选择器

| 选择器            | 示例         | 示例说明                               | CSS版本 |
| ----------------- | ------------ | -------------------------------------- | ------- |
| `.class`          | `.intro`     | 选择所有`class=intro`的元素            | 1       |
| `#id`             | `#firstname` | 选择所有`id=firstname`的元素           | 1       |
| `*`               | `*`          | 选择所有元素                           | 2       |
| `element`         | `p`          | 选择所有`<p>`元素                      | 1       |
| `element,element` | `div,p`      | 选择所有`<div>`和`<p>`元素             | 1       |
| `element element` | `div p`      | 选择`<div>`元素里的所有`<p>`元素       |         |
| `element>element` | `div>p`      | 选择所有父级是`<div>`元素的`<p>`元素   |         |
| `element+element` | `div+p`      | 选择所有紧贴`<div>`元素之后的`<p>`元素 |         |

