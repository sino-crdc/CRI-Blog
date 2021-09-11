+++
title= "微信小程序｜基础"
description = ""
summary = ""
toc = true
authors = [ "zzzsy"]
tags = ["微信小程序"]
categories = []
series = ["小程序"]
date= "2021-05-02"
lastmod = "2021-06-13"
draft = false

+++

微信小程序的基础

<!--more-->

## 配置文件

### 全局配置文件——app.json

[开发者文档](https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html)

#### pages字段

描述所有的页面路径，对应小程序的页面`pages`

对应的value是`pages/index/index`，**无后缀名**

+ 在开发者工具中直接添加语句就可以创建文件

+ `pages`中的一个语句对应打开的默认界面（否则可以使用`entryPagePath`属性）

####  windows字段

定义小程序所有页面的状态栏、导航条、标题、窗口背景色等

常见属性

+ `navigationBarBackgroundColor` 导航栏文字内容 
+ `navigationBarTitleText` 导航栏文字内容
+ `navigationBarTextStyle` 导航栏标题颜色（black/white）
+ `enablePullDownRefresh` 是否开启全局的下拉刷新
+ `backgroundTextStyle` 下拉 loading 的样式，仅支持 `dark` / `light`
+ `backgroundColor` 窗口的背景颜色（下拉后三个小圆点的背景）

#### tabBar字段

定义多tab应用的表现

+ `color` tab上的文字颜色
+ `selectedColor` tab上的文字选中时的颜色
+ `backgroundColor` tab背景色
+ `list` tab的列表，最少两个，最多五个
  + `pagePath` 已经在pages中定义的页面路径
  + `text` tab上的按钮文字
  + `iconPath` 图片路径
  + `selectedIconPath` 选中时的图片路径

### 页面配置文件——page.json

[开发者文档](https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/page.html)

单独配置页面的属性

只能配置`app.json`中的`windows`部分，会覆盖`app.json`中的配置

### sitemap配置——sitemap.json

[开发者文档](https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/sitemap.html)

配置小程序及其页面是否允许被微信索引

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

## 列表渲染

+ `wx:for`

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

+ 对象循环

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

### `block`

占位符一样的标签

写代码时，可以看到标签

页面渲染时，会被移除（使用`for`循环时）

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

# 自定义组件

> 增加代码复用性

## 创建自定义组件

+ 结构

```text
component
    ｜
   xxx -
       ｜
       ｜ - xxx.wxml
       ｜ - xxx.js
       ｜ - xxx.wxss
       ｜ - xxx.json
```

+ 使用

  > 在使用组件的页面json文件中引用组件

  ```json
  {
      "usingComponents":{
          "xxx":"../../component/xxx/xxx"
      }
  }
  ```

  
