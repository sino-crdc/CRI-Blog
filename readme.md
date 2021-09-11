### Blog 结构说明

+ assets——存放部分公共资源包括：头像、样式、Logo等
+ config——模版配置包括菜单、语言等
+ content——主要内容
  + authors——作者
  + homepage——主页
  + others——其他
  + posts——提交的笔记
  + projects——项目成果
+ data——资源文件
+ i18n——语言文件
+ layouts——模版
+ public——发布的保留文件

 ### 我如何提交自己的笔记？

1. fork 本仓库并clone至本地
2. 在content文件夹中按照example创建自己的作者文件夹，并在assets/avatar中加入自己的头像文件（.png格式）
3. 在content/posts中创建或者选择已经创建好的分类文件夹（如NLP），复制content/example/index.md到其中，并重命名为×××.md（建议不含中文）。
4. 修改文件头部的meta（两行加号之间部分），并加上自己的正文。
5. 建议使用`hugo server`命令查看效果（见[这里](#hugo本地预览)）
6. 提交到自己的仓库并start一个pull request

### `meta`参数释义

```markdown
+++
title= "example title"
description = "there is the desp"
summary = ""
toc = true //是否开启目录
authors = [ "example"]//多个作者可以用逗号隔开
tags = ["example", "example2"]
categories = []
series = ["example"]//将文章加入一个系列
date= "2021-01-22"
lastmod = "2021-01-31"
draft = false //设置为true就不会编译
+++

这里是预览的描述
This article offers a sample of basic Markdown syntax that can be used in Hugo content files, also it shows whether basic HTML elements are decorated with CSS in a Hugo theme.
<!--more-->
```

### hugo本地预览

在[这里](https://github.com/gohugoio/hugo/releases)下载对应系统的二进制包，以windows为例将得到的exe文件放到CRI-Blog文件夹下，cmd运行`hugo server`，在浏览器输入127.0.0.1:1313就可以预览了

