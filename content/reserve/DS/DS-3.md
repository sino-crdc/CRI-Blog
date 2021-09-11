+++
title= "数据结构与算法-3：线性表"
description = ""
summary = ""
toc = true
authors = [ "zhang"]
tags = ["数据结构与算法", "笔记"]
categories = []
series = ["数据结构与算法"]
date= "2021-09-04"
lastmod = "2021-09-04"
draft = false

+++

数据结构与算法-3：线性表
<!--more-->

# 线性表

## 定义

线性表是具有**相同**数据类型的$n(n\geq0)$个**数据元素**的**有限序列**，其中$n$为表长，当$n$为$0$时线性表是一个**空表**。一般表示为$L=(a_1,a_2,\cdots,a_i,a_{i+1},\cdots,a_n)$ \

> 一些基本操作

[![h2Kge0.png](https://z3.ax1x.com/2021/09/04/h2Kge0.png)](https://imgtu.com/i/h2Kge0)

+ 线性表的位序从1开始，而不是像数组一样从0开始

## 顺序表

用顺序存储的方式来实现线性表

### 实现方式

#### 静态分配

```c
#define MaxSize 10
typedef struct{
    ElemType data[MaxSize];
    int length;
}SqList;
```

最大长度不可改变（静态）

+ 初始化

  ```c
  void InitList(SqList &L){
      for (int i=0; i<MaxSize; i++){
          L.data[i]=0;
      }
      L.length=0;//初始长度为0
  }
  ```

  + 必须声明长度为0
  + 访问时要求不超过长度，因此初始化成0可以省略（编译器一般会初始化）

#### 动态分配

```c
#define InitSize 10
typedef struct{
    ElemType *data;
    int MaxSize;
    int length;
}SeqList;
```

动态申请和释放内存空间

C——`malloc` `free`

`L.data=(ElemType*)malloc(sizeof(ElemType)*InitSize);`

申请一片连续的空间

> `malloc`返回一个指针，强制转换

C++——`new` `delete`

+  增加动态数组的长度

  ```c
  void IncreaseSize(SeqList &L, int len){
      int* p = L.data;
      L.data=(int*)malloc((L.Maxsize+len)*sizeof(int));
      for(int i=0;i<L.length;i+=){
          L.data[i]=p[i];
      }
      L.MaxSize=L.MaxSize+len;
      free(p);
  }
  ```

  

### 顺序表的特点

+ **随机访问**：可以在$O(1)$时间内找到第i个元素
+ 存储密度高
+ 拓展容量不方便（动态时需要复制，**时间开销大**）
+ 插入等操作不方便

### 基本操作

#### 插入

`ListINsert(&L, i, e)`， 在表L的第i个位置插入元素e

```c
#define MaxSize 10
typedef struct{
    int data[MaxSize];
    int length;
}SqList;

void ListInsert(SqList &L, int i, int e){
    ///⭐️
    //从最后一位到插入点依次向后挪
    for(int j=L.length;j>=i;j--){
        L.data[j]=L.data[j-1];
    }
    L.data[i-1]=e;
    L.length++;
}

```

为了使得代码具有“健壮性”，应该在⭐️处插入对i的判断，并返回bool型

```c
bool ListInsert(SqList &L, int i, int e){
    if (i<1 || i>L.length+1)
        return false;
    if (L.length>=MaxSize)
        return false;
    //...
    return true
}
```

时间复杂度$O(n)$

#### 删除

```c
bool ListDelete(SqList &L, int i, int &e){
    if (i<1 || i>L.length)         //判断有效性
        return false;
    e=L.data[i-1];                 //将被删除的元素赋值给e
    for (int j=i;j<L.length;j++)
        L.data[j-1]=L.data[j];
    L.length--;
    return true;
}
```

#### 查找

##### 按位查找

  ```c
  ElemType GetElem(SqList L, int i){
      return L.data[i-1];
  }
  ```


##### 按值查找

  ```c
  int LocateElem(SeqList L, int e){
      for (int i=0;i<L.length;i++)
          if(L.data[i]==e)
              return i+1;
      return 0;
  }
  ```

  

## 单链表

链式存储的线性表

### 定义

```c
typedef struct LNode{
    ElemType data;
    struct LNode *next;
}LNode, *LinkList;
```

> `typedef <数据类型> <别名>`
>
> 在这里，`LNode` 强调结点而 `LinkList` 强调链表
>
> 声明一个指向单链表第一个结点的指针可以`LNode * L`; 或者 `LinkList L;`

### 初始化

#### 不带头结点

```c
typedef struct LNode{
    ElemType data;
    struct LNode* next;
}LNode, *LinkList;

bool InitList(LinkList &L){
    L=NULL;
    return true;
}
```

空表判断：`L==NULL`

#### 带头结点

```c
typedef struct LNode{
    ElemType data;
    struct LNode* next;
}LNode, *LinkList;

bool InitList(linkList &L){
    L = (LNode*)malloc(sizeof(LNode));
    if(L==NULL)
        return false;
    L->next = NULL;
    return true;
}
```

空表判断：`L->next==NULL`

### 基本操作

#### 插入

##### 按位序插入

+ 带头结点

  ```c
  bool ListInsert(linkList &L, int i, ElemType e){
      if(i<1)
          return false;
      LNode *p;
      int j=0;
      p = L;
      //循环找到第i-1个结点
      while (p!=NULL && j<i-1){
          p=p->next;
          j++;
      }
      if (p==NULL)//i值不合法（超出了）
          return false;
      LNode *s=(LNode*)malloc(sizeof(LNode));
      s->data=e;
      s->next=p->next;
      p->next=s;
      return true;
  }
  ```

+ 不带头结点

  对第一个结点进行处理

##### 指定节点后插操作

```c
bool InsertNextNode(LNode *p, ElemType e){
    if (p==NULL)
        return false;
    LNode *s = (LNode*)molloc(sizeof(LNode));
    if (s==NULL)
        return false;
    s->data=e;
    s-next=p->next;
    p->next=s;
    return true;
}
```

##### 指定结点的前插操作

```c
bool InsertPriorNode (Lnode *p, ElemType e){
    if (p==NULL)
        return false;
    LNode *s = (LNode*)malloc(sizeof(LNode));
    if (s==NULL)      //内存分配失败
        return false;
    s->next=p->next;
    p->next=s;        //新结点连到p之后
    s->data=p->data;  //将p中元素复制到s中
    p->data=e;        //p中元素覆盖为e
    return true;
}
```

#### 删除

##### 按位序删除

```c
bool ListDelete(LinkList &L, int i, ElemType &e){
    if (i<1)
        return false;
    LNode *p;
    int j=0;
    p = L;
    while (p!=NULL && j<i-1){
        p=p->next;
        j++;
    }
    if (p==NULL)
        return false;
    if (p->next==NULL)
        return false;
    LNode *q=p->next;
    e=q->next;
    p->next=q->next;
    free(q);
    return true;
}
```

##### 指定结点删除

```c
bool DeleteNode(LNode *p){
    if (p==NULL)
        return false;
    LNode *q=p->next;
    p->data=p->next->data;
    p->next=q->next;
    free(q);
    return true;
}
```

> 代码不能删除最后一个结点（只能从前往后找）

#### 查找

##### 按位查找

```c
LNode * GetElem(LinkList L, int i){
    if (i<0)
        return NULL;
    LNode *p;
    int j=0;
    p = L;
    while (p!=NULL && j<i){
        p=p->next;
        j++;
    }
    return p;
}
```

##### 按值查找

```c
LNode * LocateElem(LinkList L, ElemType e){
    LNode *p = L->next;
    while (p !=NULL && p->data != e)
        p=p->next;
    return p;
}
```

### 单链表的建立

> 初始化一个表
>
> 每次取一个数据元素，插入

#### 尾插法

```c
LinkList List_TailInsert(LinkList &L){
    int x;
    L=(LinkList)malloc(sizeof(LNode));    //建立头结点
    LNode *s, *r=L;            //r是表尾指针
    scanf("%d", &x);
    while(x!=9999){
        s=(LNode*)malloc(sizeof(LNode));
        s->data=x;
        r->next=s;
        r=s;                  //r指向新的表尾
        scanf("%d", &x);
    }
    r->next=NULL;             //r指针置空
    return L;
}
```

#### 头插法

```c
LinkList List_HeadInsert(LinkList &L){
    LNode *s;
    int x;
    L=(LinkList)malloc(sizeof(LNode));    //建立头结点
    L->next=NULL;             //！初始为空
    scanf("%d", &x);
    while(x!=9999){
        s=(LNode*)malloc(sizeof(LNode));
        s->data=x;
        s->next=L->next;
        L->next=s;                  //插入新结点
        scanf("%d", &x);
    }
    return L;
}
```

主要应用于**链表的逆置**
