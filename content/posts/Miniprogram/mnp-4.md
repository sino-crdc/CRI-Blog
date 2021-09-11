

+++
title= "微信小程序｜样式"
description = ""
summary = ""
toc = true
authors = [ "zzzsy"]
tags = ["微信小程序"]
categories = []
series = ["小程序"]
date= "2021-05-16"
lastmod = "2021-05-19"
draft = false

+++

微信小程序的语法基础

<!--more-->

# 样式WXSS

## 尺寸单位

`rpx`：可以根据屏幕宽度进行自适应。规定宽度为`750rpx` 。`1rpx = 0.5px = 1物理像素`

`.wxss`

```css
/*
  1 小程序中，不需要主动引入样式文件
  2 rpx可以自适应
  3 计算时，利用属性 calc
    1 可以使用百分比、px、em、rem等单位
    2 可以混合使用各种单位进行计算
    3 表达式中用`+`和`-`时，其前后必须油空格
    4 表达式中有`*`和`/`时，其前后可以没有空格，但建议保留
*/
view{
    width: calc(750rpx * 100 / 375);
    height: 200rpx;
    font-size: 40rpx;
    background-color: aqua;
}
```

`.wxml`

```html
<view> 
  rpx
</view>
```

设计稿 `page px` ， 存在一个元素`100 px`

适配不同界面时

`100 px = 750 rpx * 100 / page`

## 样式导入

使用`@import`导入，只支持**相对路径**

例如：

```css
@import "../../styles/common.wxss";
```

## 选择器

小程序不支持通配符`*` ！

支持的选择器有

| 选择器           | 样例              | 描述                             |
| ---------------- | ----------------- | -------------------------------- |
| .class           | `.intro`          | 选择所有拥有 class=“intro”的组件 |
| #id              | `#firstname`      | 选择拥有 id=“firstname”的组件    |
| element          | `view`            | 选择所有view组件                 |
| element, element | `view, checkbox`  | 选择所有view和checkbox组件       |
| nth-child(n)     | view:nth-child(n) | 选择某个索引的标签               |
| ::after          | `view::after`     | 在view组件后插入内容             |
| ::before         | `view::before`    | 在view组件前插入内容             |

## 使用less

`vscode` 使用 `easy less` 插件

配置文件中写

```json
"less.compile":{
    "outExt": ".wxss"
}
```

