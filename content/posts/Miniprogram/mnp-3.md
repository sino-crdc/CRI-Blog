

+++
title= "微信小程序｜条件渲染和事件绑定"
description = ""
summary = ""
toc = true
authors = [ "zzzsy"]
tags = ["微信小程序"]
categories = []
series = ["小程序"]
date= "2021-05-12"
lastmod = "2021-05-13"
draft = false

+++

微信小程序的语法基础

<!--more-->

### `block`

占位符一样的标签

写代码时，可以看到标签

页面渲染时，会被移除（使用`for`循环时）

## 条件渲染

### `wx:if`

使用`wx:if="{{condition}}"`来

```html
<view> 
    <view> 条件渲染 </view>
    <view wx:if="{{true}}"> 显示 </view>
    <view wx:if="{{false}}"> 隐藏 </view>
</view>
```

`if`  `else`语法——`wx:if` `wx:elif` `wx:else`

### `hidden`属性

```html
<view hidden> 隐藏 </view>
<view hidden="{{true}}"> 隐藏 </view>
<view hidden="{{false}}"> 显示 </view>
```



> 当标签不是频繁地切换显示时 优先使用 `wx:if` （直接移除代码）
>
> 当标签需要频繁地切换显示时 优先使用 `hidden` （添加隐藏样式）

> `hidden`属性不要和`diplay`样式一起使用



## 事件绑定

#### 双向绑定

`.js`

```js
Page({
    data:{
        num: 0
    },
    //input事件的执行
    handleInput(e){
        //console.log(e);
        this.setData({
        num: e.detail.value
    })
    }
})
```

`.html`

```html
<!--
  1 需要给input标签绑定一个input事件
    绑定关键字 bindinput
  2 获取输入框的值
    e.detail.value
  3 把输入框的值 赋到data
    this.setData({
        num:e.detail.value
    })
-->
<input type="text" bindinput="handleInput" />
<view>  
  {{num}}
</view>
```

#### 绑定一个按钮

```js
Page({
    //
    handletap(e){
        //console.log(e);
        const operation=e.currentTarget.dataset.operation;
        this.setData({
            num: this.data.num + operation
        })
    }
})
```

```html
<!--
  1 需要加入一个点击事件
    1 bindtap
    2 无法在小程序的事件中直接传参
    3 在属性中自定义 来传参
    4 事件源中获取参数
-->
<input type="text" bindinput="handleInput" />
<button bindtap="handletap data-operation="{{1}}>+</button>
<button bindtap="handletap data-operation="{{-1}}>-</button>
<view>  
  {{num}}
</view>
```

