

+++
title= "微信小程序 ｜ 常见组件"
description = ""
summary = ""
toc = true
authors = [ "zhang"]
tags = ["微信小程序", "笔记"]
categories = []
series = ["小程序"]
date= "2021-05-20"
lastmod = "2021-05-23"
draft = false

+++

微信小程序的语法基础

<!--more-->

# 常见组件

## `view`标签

代替原来的 `div` 标签

## `text`标签

+ 文本标签
+ 只能嵌套text
+ 可以实现文字复制（只有这个标签）
+ 可以对空格、回车进行编码

| 属性        | 默认  | 说明         |
| ----------- | ----- | ------------ |
| user-select | false | 文字是否可选 |
| decode      | false | 是否解码     |

## `image`标签

+ image组件的默认宽度是320px、高度是240px

+ 支持lazy 加载：当图片出现在某个高度之内时，自动开始加载

+ 一些属性

  | 属性      | 说明                     |
  | --------- | ------------------------ |
  | src       | 指定图片加载路径         |
  | lazy-load | 图片懒加载               |
  | mode      | 指定图片裁剪、缩放的形式 |


+ 常见mode的值

  | 值          | 说明                                                         |
  | ----------- | ------------------------------------------------------------ |
  | scaleToFill | 缩放模式，不保持纵横比缩放图片，使图片的宽高完全拉伸至填满 image 元素 |
  | aspectFit   | 缩放模式，保持纵横比缩放图片，使图片的长边能完全显示出来。也就是说，可以完整地将图片显示出来。 |
  | widthFix    | 缩放模式，宽度不变，高度自动变化，保持原图宽高比不变         |
  | heightFix   | 缩放模式，高度不变，宽度自动变化，保持原图宽高比不变         |
  | aspectFill  | 缩放模式，保持纵横比缩放图片，只保证图片的短边能完全显示出来。也就是说，图片通常只在水平或垂直方向是完整的，另一个方向将会发生截取。 |

+ image组件中的二维码、小程序码不支持长按识别

## `swiper` 组件

轮播图

+ 轮播图外层容器：`swiper`
+ 每一个轮播项： `swiper-item`
+ 默认样式
  + width 100%
  + height 150px
  + swiper 高度 无法由内容撑开
+ 先找原图的宽高，等比例计算swiper的宽高
  + swiper 宽度 = 100vw × 原图高度 / 原图的宽度

`.wxml`

```html
<swiper>
  <swiper-item> <image mode="widthFix" src="....." /> </swiper-item>
  <swiper-item> <image mode="widthFix" src="....." /> </swiper-item>
  <swiper-item> <image mode="widthFix" src="....." /> </swiper-item>
</swiper>
```

`.wxss`

```css
swiiper{
    width: 100%;
    height: calc(100vw * 352 / 1125);
}
image{
    width: 100%;
}
```

> “视区”：浏览器内部可视区域的大小
>
> “vw”：1vw等于视图窗口宽度的1%

### swiper常见属性

| 属性                   | 类型    | 默认值        | 说明             |
| ---------------------- | ------- | ------------- | ---------------- |
| indicator-dots         | Boolean | false         | 显示指示点       |
| indicator-color        | Color   | rgba(0,0,0,3) | 指示点颜色       |
| circular               | Boolean | false         | 循环轮播         |
| autoplay               | Boolean | false         | 自动轮播         |
| interval               | Number  | 5000          | 修改轮播时间     |
| indicator-active-color | Color   | #000000       | 选中指示点的颜色 |

## `navigator`标签

导航组件



```html
<!--
  0 块级元素
  1 url 要跳转的要页面路径
  2 target 跳转的页面（self/miniProgram）：自己或其他小程序
  3 open-type 
-->

<navigator url="/.../.../..."> 下个界面 </navigator>
```

open-type的有效值

| 值           | 说明                                           |
| ------------ | ---------------------------------------------- |
| navigate     | 保留当前页面，跳转到除了tabbar的应用内其他页面 |
| redirect     | 关闭当前页面，跳转到除了tabbar的应用内其他页面 |
| switchTab    | 跳转到tabbar页面，并关闭其他非tabbar页面       |
| reLaunch     | 关闭所有界面，打开到应用内的某个界面           |
| navigateBack | 关闭当前页面，返回一级或多级页面               |
| exit         | 退出小程序                                     |

## `rich-text`标签

[开发者文档](https://developers.weixin.qq.com/miniprogram/dev/component/rich-text.html)

富文本标签：将字符串解析为

```html
<!--
  1 nodes属性来实现
    1 接收标签字符串
    2 接收对象数组
-->
```

`.js`

```js
Page({
    data:{
        //1 标签字符串
        //html:'......'
        //2对象数组
        html:[
            //1 div标签 name属性来指定
            name:"div",
            //标签上有哪些属性
            attrs:{
              //标签上的属性 class style
              class:"my_div",
              style:"color:red;"
            },
            //3 子节点 children 要接收的数据类型和nodes第二种渲染方式的类型一致
            children:[
                {
                    type:"text",
                    text:"hello"
                }
            ]
        ]
    }
})
```

## `button` 标签

