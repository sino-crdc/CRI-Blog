+++
title= "模型载存、Datasets 和 数据预处理"
description = ""
summary = ""
toc = true
authors = [ "ZenMoore"]
tags = ["NLP", "预处理", "pytorch"]
categories = []
series = ["AI"]
date= "2021-01-22"
lastmod = "2021-01-31"
draft = false

+++

1. 模型怎么保存？在测试或者应用是怎么使用保存好的模型？
2. 怎么将数据集输入？或者对数据集怎么进行操作？
3. 输入的数据往往是五花八门的，怎么对他们进行预处理，以方便训练和测试？

<!--more-->

## 写在前面

这次活动的内容主要是模型载存、Datasets 和 数据预处理。

之前我们介绍到，对于一个最简模型：

在训练阶段，数据集->输入->前向传播->后向传播

在测试或者应用阶段，输入->前向传播->输出

我们已经做过后向传播的扩展(学习率和优化器等)，也做过前向传播的扩展(卷积和循环等)。接下来，我们对其余的部分进行扩展，最后完成一套完整的神经网络模型。下周 TensorboardX 可视化和下下周的 hook 分别属于对前后向传播过程的显示和操作。

扩展后的流程如下：

训练流程：数据预处理->数据集->输入->前向传播->损失函数->反向传播训练->若干轮训练->保存模型备用

测试/应用流程：测试集或待测数据->数据预处理->输入->前向传播(已加载好模型)->输出

我们今天解决三个问题：

1. 模型怎么保存？在测试或者应用是怎么使用保存好的模型？
2. 怎么将数据集输入？或者对数据集怎么进行操作？
3. 输入的数据往往是五花八门的，怎么对他们进行预处理，以方便训练和测试？

## 模型载存

保存和加载的 PyTorch 代码很简单

```python
# 保存和加载整个模型
torch.save(model_object, 'model.pkl')
model = torch.load('model.pkl')

# 仅保存和加载模型参数（常用）
torch.save(model_object.state_dict(), 'params.pkl')
model_object.load_state_dict(torch.load('params.pkl'))
```

加载整个模型：operating graph + parameters

仅加载参数：parameters

所以一般来说：

当加载整个模型时候，在测试代码中不需要重新定义网络结构

当仅加载参数时候，需要在测试代码中重新定义网络结构

## Datasets

分三步说：为什么要有Datasets? 怎么定义Datasets? 怎么使用Datasets?

### 为什么要有 Datasets?

- 方便将数据集输入到模型中
- 方便划分数据集为测试集、验证集和训练集
- 方便数据集的处理(数据预处理)
- ......

### 怎么定义 Datasets?

我们以图像数据集的构建为例：

下面补充几个概念

`数据增强：比如数据集原来有10张照片，我们将它颠倒、缩放、旋转、剪裁等扩充成100张照片，因为无论一只猫是正着的还是倒着的，我们都能够识别出它是猫，因此我们希望通过数据集的扩充，一方面增加数据，另一方面利用这种不变性`

`别忘了标签：一个数据example是以(data, label)对的形式出现的`

`torchvision.transforms: 用于图像处理的一个包，待会儿用代码说`



```python
from torch.utils.data import Dataset
from torch.utils.data import DataLoader

class MyDataset(Dataset):
    """
     root: 图像存放地址根路径
     augment：是否需要图像增强
    """
    
    def __init__(self, root, augment=None):
        # 这个 list 存放所有图像的地址
        self.image_files = np.array([
            x.path for x in os.scandir(root)
            if x.name.endswith(".jpg") or x.name.endswith(".png") or x.name.endswith(".JPG")
        ])
        self.augment = augment
       
    
    def __getitem__(self, index):
        if self.augment:
            image = open_image(self.image_files[index])   # 这里的 open_image 是读取图像的函数，可以用 PIL 或者 OpenCV 等库进行读取
            image = self.augment(image)	  # 这里对图像进行了数据增强
            return to_tensor(image)	      # PyTorch 中得到的图像必须是 tensor
        else:
            image = open_image(self.image_files[index])
            return to_tensor(image)
```

### 怎么使用 Datasets?

```python
from torch.utils.data import Dataset
from torch.utils.data import DataLoader

#这里是 Datasets 定义

datasets = MyDataset(root='./allset/', augment=None)
dataloader = DataLoader(datasets, batch_size=128, shuffle=True)

num_epoches = 100
for epoch in range(num_epoches):
    for img, label in dataloader:
        #这里是训练的代码
        pass
```

## 数据预处理

首先要区分训练阶段和测试阶段的数据预处理有差异性也有一致性

差异性：为了扩充训练数据集而进行的数据增强操作不必用于测试集，因为测试/应用时，你要判断一张图片的类别时不必将其颠倒旋转，而进行训练时为了尽可能地保证图片旋转后仍可识别，需要用旋转前后的图片共同训练。

一致性：尽量保证训练时数据的格式和测试/应用时数据的格式是一样的。

要满足这种差异性的数据预处理有数据增强等，但这不是数据预处理的重点！

数据预处理的重点在于需要满足一致性的一类，下面举几个例子：

1. 去除唯一属性：如id等，对分类没什么用
2. 缺失值处理：直接删除带缺失值的数据或者进行补全

`补全技术也是很有意思的一个问题，这个问题经常出现，常用的解决方式有：压缩感知见《机器学习》(周志华)等，也可以尝试使用因果推理(Causal Inference)的技术进行补全如 ATE with adjust/control for confounders 方法,感兴趣的同学可以参阅《Introduction to Causal Inference (ICI)
from a Machine Learning Perspective》(Brady Neal)`

3. 归一化：如将数据统一缩放到[0,1]的范围等
4. 降维技术：如 LDA, PCA 等，见《机器学习》(周志华)
5. 稀疏表示、字典学习等等，见《机器学习》(周志华)
6. 去除数据冗余性：白化等

例如，在手势识别项目中进行的三个简单的数据预处理：

1. 卷积降噪

```python
    for i in range(6):
        X = data[i]
        wave = np.ones(FILTER_SIZE)*SIGNAL_AMP
        data[i] = np.convolve(X, wave, 'same')
    return data
```

2. 零均值化

```python
    for i in range(6):
        data[i] -= np.mean(data[i], axis=0)
    return data
```

3. 归一化

```python
    for i in range(6):
        data[i] /= np.std(data[i], axis=0)
    return data
```

`数据预处理是一门很深的学问，需要大量的理论基础，可以说，这是机器学习中一个很重要的子领域，大家一定要注重在平时的学习和实践中不断积累此类知识。`

## 下期预告：

觉得训练很抽象？print 出来的 loss 数字不直观？用 TensorboardX 把深度学习画出来吧！

hook 是什么？它是怎么像百里玄策一样在前向传播和后向传播的数据流里把参数钩来钩去的？
