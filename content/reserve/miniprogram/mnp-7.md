

+++
title= "微信小程序 | 实践项目笔记（1）-- css部分"
description = ""
summary = ""
toc = true
authors = [ "zhang"]
tags = ["微信小程序", "笔记"]
categories = []
series = ["小程序"]
date= "2021-08-20"
lastmod = "2021-08-22"
draft = false

+++

微信小程序项目实践中关于wxss的一些笔记

<!--more-->
## 基础知识

### 盒子模型（box model）

基本分为四部分：

- **Margin(外边距)** - 清除边框外的区域，外边距是透明的。
- **Border(边框)** - 围绕在内边距和内容外的边框。
- **Padding(内边距)** - 清除内容周围的区域，内边距是透明的。
- **Content(内容)** - 盒子的内容，显示文本和图像。

### 边框（border）

+ **`border-style`**：none、dotted、dashed、solid，double

+ **`border-width`**
+ **`border-color`**

> 可以在中间加入方向指示某一边框 如 `border-right-color`
>
> 采用简写模式：**`border: 2px solid #fff `**

### 外边距（margin）

指定元素周围的空间

### 阴影（box-shadow）

`box-shadow: h-shadow v-shadow blur spread color inset;`

| 属性值   | 说明                                              |
| -------- | ------------------------------------------------- |
| h-shadow | 必需的。水平阴影的位置。允许负值                  |
| v-shadow | 必需的。垂直阴影的位置。允许负值                  |
| blur     | 可选。模糊距离                                    |
| spread   | 可选。阴影的大小                                  |
| color    | 可选。阴影的颜色。在CSS颜色值寻找颜色值的完整列表 |
| inset    | 可选。从外层的阴影（开始时）改变阴影内侧阴影      |

```less
.md{
    box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}
```

## 弹性盒子（flex box）

一种好用的布局模型

> 弹性盒子由弹性容器(Flex container)和弹性子元素(Flex item)组成。
>
> 弹性容器通过设置 display 属性的值为 flex 或 inline-flex将其定义为弹性容器。

+ **`flex-direction`**：定义排列方向

  `flex-direction: row | row-reverse | column | column-reverse`

+ **`justify-content`**：定义内容对齐（沿主轴线）

  `justify-content: flex-start | flex-end | center | space-between | space-around`

  [![hSrHln.jpg](https://z3.ax1x.com/2021/08/22/hSrHln.jpg)](https://imgtu.com/i/hSrHln)

+ **`align-items`**：定义内容对齐（沿侧轴）

  `align-items: flex-start | flex-end | center | baseline | stretch`

+ **`flex`**：定义占比

  ```less
  .wrap{
      display: flex;
      .item1{
          flex: 2;
      }
      .item2{
          flex: 3;
      }
  }
  ```

+ **`flex-wrap`**：定义是否换行

## 一些操作

### 同一属性的不同方向设置

```css
style：attr1，attr2，attr3，attr4
/*上->右->下->左*/
style：attr1，attr2，attr3
/*上->左右->下*/
style：attr1，attr2
/*上下->左右*/
style：attr1
/*上下左右属性相同*/
```

### 页脚定位

```css
.foot{
    position: absolute;
    buttom: 28rpx;
    text-align: center;
}
```

### 圆形Logo

```css
.logo{
    border-radius: 50%;
}
```

### 选择器

  + less语法中：`&`代表上一级父元素
  + `:nth-of-type(1)`可以选择第几个元素

  ```less
  .content{
          margin: 4rpx 25rpx;
          flex:1;
          font-size: 30rpx;
          color: var(--commentColorLight);
          &:nth-of-type(1){
              margin-top: 25rpx;
          }
          &:nth-last-of-type(1){
              margin-bottom: 25rpx;
          }
      }
  ```

### 只显示几行字

  + **`word-break`**：自动换行的方式

    | 属性值    | 说明                         |
    | --------- | ---------------------------- |
    | normal    | 使用默认的换行规则           |
    | break-all | 允许在单词内换行             |
    | keep-all  | 只能在半角空格或连字符处换行 |

  + **`text-overflow`**：规定当文本溢出包含元素时发生的事情

    | 属性值   | 说明                           |
    | -------- | ------------------------------ |
    | clip     | 修剪文本                       |
    | ellipsis | 使用省略号表示被修剪的文本     |
    | string   | 使用给定的符号表示被修剪的文本 |


  ```less
  .meta {
      width: 100%;
      margin-left: 6rpx;
      font-size: 28rpx;
      color: #888888;
      font-size: 28rpx;
      /*自动换行*/
      display: -webkit-box;
      word-break: break-all;
      text-overflow: ellipsis;  
      overflow: hidden;
      -webkit-box-orient: vertical;
      -webkit-line-clamp: 2;       /*定义可以显示几行*/
      }
  ```

### 定义全局变量

可以在app.wxss定义全局的变量

  ```less
  page{
      --themeColor: #1296db; 
  }
  ```

  然后在页面page.wxss使用

  ```less
  .item{
      color: var(--themeColor)
  }
  ```

### 自定义按钮样式

  ```less
  .btn{
      height: 160rpx;
      width: 200rpx;
      margin: 0 60rpx;
      border-radius: 16rpx;
      background-color: #fff;
      display: flex;
      justify-content: center;
      &::after {
        border: 0;/*requied*/
        border-radius: 16rpx;
      }
  }
  .btn_hover{
      /*要使用!important*/
      background-color: #f4f4f4 !important;
      opacity: 0.9 !important;
  }
  ```

  在wxml文件中定义`hover`样式

  ```html
  <button bind:tap="onEdit" hover-class="btn_hover">
  ```

  

  
