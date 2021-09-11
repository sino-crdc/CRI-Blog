+++
title= "微信小程序｜配置文件"
description = ""
summary = ""
toc = true
authors = [ "zzzsy"]
tags = ["微信小程序"]
categories = []
series = ["小程序"]
date= "2021-05-02"
lastmod = "2021-05-05"
draft = false

+++

微信小程序的配置文件：全局配置、页面配置、sitemap配置

<!--more-->

## 全局配置文件——app.json

[开发者文档](https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html)

### pages字段

描述所有的页面路径，对应小程序的页面`pages`

对应的value是`pages/index/index`，**无后缀名**

+ 在开发者工具中直接添加语句就可以创建文件

+ `pages`中的一个语句对应打开的默认界面（否则可以使用`entryPagePath`属性）

###  windows字段

定义小程序所有页面的状态栏、导航条、标题、窗口背景色等

常见属性

+ `navigationBarBackgroundColor` 导航栏文字内容 
+ `navigationBarTitleText` 导航栏文字内容
+ `navigationBarTextStyle` 导航栏标题颜色（black/white）
+ `enablePullDownRefresh` 是否开启全局的下拉刷新
+ `backgroundTextStyle` 下拉 loading 的样式，仅支持 `dark` / `light`
+ `backgroundColor` 窗口的背景颜色（下拉后三个小圆点的背景）

### tabBar字段

定义多tab应用的表现

+ `color` tab上的文字颜色
+ `selectedColor` tab上的文字选中时的颜色
+ `backgroundColor` tab背景色
+ `list` tab的列表，最少两个，最多五个
  + `pagePath` 已经在pages中定义的页面路径
  + `text` tab上的按钮文字
  + `iconPath` 图片路径
  + `selectedIconPath` 选中时的图片路径

## 页面配置文件——page.json

[开发者文档](https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/page.html)

单独配置页面的属性

只能配置`app.json`中的`windows`部分，会覆盖`app.json`中的配置

## sitemap配置——sitemap.json

[开发者文档](https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/sitemap.html)

配置小程序及其页面是否允许被微信索引

