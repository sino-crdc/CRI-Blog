

+++
title= "微信小程序｜自定义组件"
description = ""
summary = ""
toc = true
authors = [ "zzzsy"]
tags = ["微信小程序"]
categories = []
series = ["小程序"]
date= "2021-07-20"
lastmod = "2021-07-23"
draft = false

+++

微信小程序的语法基础

<!--more-->

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

  
