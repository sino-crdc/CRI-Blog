

+++
title= "微信小程序｜数据绑定、运算和循环"
description = ""
summary = ""
toc = true
authors = [ "zzzsy"]
tags = ["微信小程序"]
categories = []
series = ["小程序"]
date= "2021-05-07"
lastmod = "2021-05-09"
draft = false

+++

微信小程序的语法基础

<!--more-->

## 模版语法

### 数据绑定

#### 普通写法

`text`标签相当于`span`标签：行内元素

`view`标签相当于`div`标签：块级元素

#### 数据绑定

`.js`文件

```javascript
Page({
    data: {
        msg: "hello",
        num: 10000,
        person:{
            age:74,
            height:176,
            name:"Paul"
        },
        isChecked:false
    }
})
```

`.wxml`文件

```html
<view> {{msg}} </view>
<view> {{person.age}} </view>
<view data-num="{{num}}" > 自定义属性 </view>
<view>
    <checkbox checked="{{isChecked}}" >  </checkbox>
    <!--引号与括号间不能有空格-->
</view>
```

## 运算

> 可已在花括号中加入一些表达式

```html
<!--数字运算-->
<view> {{1+1}} </view>
<!--字符串拼接-->
<view> {{'1'+'1'}} </view>
<!--三目表达式-->
<view> {{ 10%2===0 ? '偶数' : '奇数'}} </view>
<!--三个’=’是严格等于，即值相等，数据类型也相等-->
```

### 列表渲染

#### `wx:for`

项的变量名默认为`item` `wx:for-item`可移指定当前元素的变量名

下标变量名默认为`index` `wx:for-index`可以指定当前下标的变量名

`.js`

```javascript
list:[
    {
        id:0,
        name:"A"
    },
    {
        id:1,
        name:"B"
    },
    {
        id:2,
        name:"C"
    }
]
person:{
    age:74,
    height:176,
    name:"Paul",
    id=1234
}
```

`.wxml`

```html
<!--
  列表循环
    1 wx:for="{{数组或对象}}" 
      wx:for-item="循环项的名称" 
      wx:for-index="索引项的索引"
    2 wx:key="唯一的值" 提高渲染性能
      使用主键或 *this
    3 循环嵌套时，名称不要重复（index，item）
    4 wx:for-item="item" wx:for-index="index"是默认值，可以不写（无嵌套时）
-->
<view> 
    <view wx:for="{{list}}" wx:for-item="item" wx:for-index="index"> 
        索引：{{index}}
        --
        值：{{item.name}}
    </view>
</view>
```

对象循环

```html
<!--wx:for-item="value" wx:for-index="key"
为了便于识别对象-->
<view> 
    <view> 对象循环 </view>
    <view
        wx:for="{{person}}"
        wx:for-item="value" 
        wx:for-index="key"
        wx:key="id">
        属性:{{value}}
        --
        值:{{key}}
    </view>
</view>
```

