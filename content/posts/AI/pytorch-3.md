+++
title= "Tensorboardx 可视化"
description = ""
summary = ""
toc = true
authors = [ "ZenMoore"]
tags = ["NLP", "tensorboard", "pytorch", "可视化"]
categories = []
series = ["AI"]
date= "2021-01-22"
lastmod = "2021-01-31"
draft = false

+++

根据塞尔认知哲学的观点，语言智能是思维智能的基础，所以个人认为 NLP 在人工智能领域的重要性是要强于 CV 的。

已经学过的 NLP 的重要模型有循环神经网络(LSTM、GRU)等，但这些都是传统的基础模型，现阶段的 NLP 离不开 attention 机制，或者说离不开 Transformer. 因为 NLP 目前 SOTA(state-of-the-art) 的模型，如 BERT、GPT-3 等，都是基于 Transformer 的。

<!--more-->

## 写在前面

这个部分的内容非常重要，可以让你了解训练到了怎样的程度。

tensorboard 原本是 tensorflow 的一个可视化，但是鉴于 PyTorch 原生的可视化工具 torchviz 不太舒服，人们将 tensorboard 迁移到了PyTorch 做了一个 tensorboardx.

这个可视化是在浏览器里面做的，你先在代码中指定好要可视化什么，运行程序，然后在终端输入命令他会给你生成一个本地的网页地址，然后打开在浏览器里面看。

更多内容大家请看 tensorboard 的官网！

## 可视化什么？

标量 scalar：记录一些标量数据，常见的如 loss 等

图片 image: 记录一些图片，用于 cv 领域

直方图 histogram: 记录一组数据的直方图，如 weight 的分布，不常用

运行图 graph : 记录运算图

嵌入向量 embedding： 记录 embedding 向量，用于 nlp 领域

`常用 scalar 和 graph, histogram/image/embedding 等未来会接触`

## 可视化的代码

SummaryWriter == 画笔！

1. 创建 SummaryWriter

```python
from tensorboardX import SummaryWriter

# Creates writer1 object.
# The log will be saved in 'runs/exp'
writer1 = SummaryWriter('runs/exp')

# Creates writer2 object with auto generated file name
# The log directory will be something like 'runs/Aug20-17-20-33'
writer2 = SummaryWriter()

# Creates writer3 object with auto generated file name, the comment will be appended to the filename.
# The log directory will be something like 'runs/Aug20-17-20-33-resnet'
writer3 = SummaryWriter(comment='resnet')
```

`一般，一次实验新建一个 run，也就是 runs/exp1, runs/exp2...`

2. 使用 SummaryWriter 对象新增可视化对象

```python
writer.add_scalar('loss', loss.item(), global_step=epoch)
writer.add_graph(myNet, input_to_model=None)

# others
writer.add_image, writer.add_histogram...
```

3. 显示命令

```cmd
tensorboard --logdir=runs/
```

## 完整项目示例

给大家看两个项目

一个是递归神经网络的计算图，一个是 embedding.
