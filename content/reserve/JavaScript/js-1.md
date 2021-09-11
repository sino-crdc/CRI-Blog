+++
title= "JS笔记-1：JS介绍"
description = ""
summary = ""
toc = false
authors = [ "zhang"]
tags = ["JS","javascript", "笔记"]
categories = []
series = ["前端"]
date= "2021-05-01"
lastmod = "2021-05-01"
draft = false

+++

<!--more-->

**JavaScript 对网页行为进行编程**  [JavaScript](https://zh.wikipedia.org/wiki/JavaScript)

它与`html`和`css`协同

> JavaScript 和 java 是在概念和设计上**完全不同**的语言 

## JavaScript使用

在 `html` 中，js代码需要位于`<script>` 与 `</script>` 中。

```html
<script>
    document.getElementById("demo").innerHTML = "改变后的内容"
</script>
```

> 旧的 JavaScript 例子也许会使用 **type** 属性：`<script type="text/javascript">`。
>
> 然而和`css`一样，这是没有必要的。

+ 把脚本置于 `<body>` 元素的底部，可改善显示速度，因为脚本编译会拖慢显示。

+ 脚本也可以防止在外部文件中，拓展名  **.js**  （不包含`<script>`）
  需要在`script`标签中使用`src`属性引用。

## JavaScript 输出

+ JavaScript **不提供**任何内建的打印或显示函数

### 显示方案

+ 使用 `windows.alert()`  写入警告框
+ 使用  `document.write()`  写入HTML输出
+ 使用  `innerHTML`  写入HTML元素
+ 使用  `console.log`  写入浏览器控制台

