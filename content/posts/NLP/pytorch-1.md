+++
title= "pytorch：模型载存、Datasets、数据预处理"
description = ""
summary = ""
toc = true
authors = [ "zzzsy"]
tags = ["pytorch", "神经网络"]
categories = []
series = ["pytorch"]
date= "2021-01-31"
lastmod = "2021-01-31"
draft = false

+++

pytorch：模型载存、Datasets、数据预处理
<!--more-->

## 模型载存

两种方法：

`torch.save(obj, dir)`

+ 保存整个模型（结构+参数）

  > 整个**model对象**

```python
#保存模型
torch.save(model_object,'model.pkl')
#加载模型
model = torch.load('model.pkl')
```
+ 只保存参数（推荐）

  > 获取model的参数 - **词典**

```python
#仅保存模型参数
torch.save(model_object.state_dict(),'params.pkl')
#仅加载模型参数
model_object.load_state_dict(torch.load('params.pkl'))

#也可以指定
save_data = {
    'model_state_dict':model.state_dict(),
    'optimzer_state_dict':optimzer.state_dict(),
    'loss':loss,
    'epoch':epoch,
    'args':args
    ···
}

```

+ 当载存整个模型的时候：只需要在训练阶段定义网络结构，在测试代码当中不需要重新定义，直接根据文件加载网络结构+参数即可
+ 当仅载存模型参数的时候，不仅需要在训练阶段定义网络结构，在测试代码中也需要，然后根据文件加载参数。



## Datasets

### 为什么要有 Datasets?

+ 方便数据集输入到模型当中
+ 方便划分数据集：训练集、测试集、验证集
+ ......

### 怎么定义 Datasets?

#### 1. Datasets 类

```python
from torch.utils.data import Dataset
from torch.utils.data import DataLoader

class MyDataset(Dataset):#继承Dataset类
    def __init__(self,dir,augment=None, transform=None):
        pass
#从datasets数据集中取读一条数据，index表示索引位置返回obj&label
    def __getitem__(self, index):
        pass
#返回数据集的总长度（训练集的总数）
    def __len__(self):
        pass
```
**数据增强( augment)**：比如数据集原来有10张照片，我们将它颜倒、旋转、缩放、剪裁等扩充100张照片，因为无论一只猫是倒着还是正着，我们都能识别出它是猫，因此我们希望通过数据集的扩充，一方面增加数据集的大小，另一方面体现这个不变性。


#### 2. 分析DataLoader

```python
train_loader = DataLoader(
    datasets.MNIST('../data', train=True, download=True,
                   transform=transforms.Compose([
                       transforms.ToTensor(),
                       transforms.Normalize((0.1307,), (0.3081,))
                   ])),
    batch_size=batch_size, shuffle=True)
```

`DataLoder(datasets,batch_size=128, shuffle = True)`

+ batch_size表示我们定义的batch大小（即每轮训练使用的批大小）
+ shuffle表示是否打乱数据顺序（对于整个datasets里包含的所有数据）

### Datasets的使用

```python
datasets = MyDataset(dir = '../data/', argument = None)
dataloader = DataLoader(datasets, batch_size = 128, shuffle = True)

num_epoches = 10000
for epoch in range(num_epoches):
    for img, label in dataloader:
        #训练（后向传播）
        pass
    pass

```

## 数据预处理

首先区分训练阶段、测试阶段数据预处理有差异性也有一致性

**差异性**：数据増强一般只用于训练集以扩充训练集满足不变性，但是在测试/应用阶段不必进行增强

**一致性**：尽量保证训练、測试/应用时候数据的格式、属性是一致的

> 举几个例子（一致性）：
>
>1. 去除唯一属性：id,对分类没什么用
>2. 缺失值处理：直接删除带缺失值的数据或者进行补全
>
>
>补全技术是一个很有意思的问题，经常出现，常见的解决方式有：压缩感知、因果推理( Causal Inference)。

