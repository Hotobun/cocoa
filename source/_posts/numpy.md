---
title: Numpy
date: 2020-1-01 18:01:17
tags: 
- python
- 数据分析
categories:
cover: /img/numpy.png
---

## numpy 数组对象 ndarray
#### 为什么使用ndarray
* 科学计算涉及数据较多,对存储和性能都有较高要求。
* 对元素类型精细定义,有助于Numpy合理使用存储空间并优化性能。
* 对元素类型精细定义,有助于对程序规模有合理评估。
* ndarray允许非同质元素构成数组（各元素类型不一致）,但无法发挥Numpy优势,尽量避免使用。

举个栗子
``` python
>>> import numpy as np

>>> a = np.array([range(5), range(5,10)])
>>> a
array([[0, 1, 2, 3, 4],
       [5, 6, 7, 8, 9]])
 
>>> print(a)
[[0 1 2 3 4]
 [5 6 7 8 9]]
  
>>> a.ndim
2
 
>>> a.shape
(2, 5)
 
>>> a.size
10
 
>>> a.dtype
dtype('int32')
 
>>> a.itemsize
4
```

#### ndarray对象常用属性

方法|说明
:---|:---
array.ndim|秩,即轴的数量或维度数量
array.shape|ndarray对象的尺度,对于矩阵,n行m列
array.size|ndarray对象元素个数,相当于.shape中n\*m的值  
array.dtype| ndarray对象的元素类型
array.itemsize|ndarray对象中每个元素的大小,以字节为单位

#### ndarray的元素类型

数据类型|说明
:---|:-
bool|布尔类型, True或False
intc|与C语言中int类型一致, 一半是int32或int64
intp|用于索引的整数, 与C语言中ssize_t一致,int32或int64
int8|字节长度的整数, 取值: [-128,127]
int16|16位长度的整数, 取值: [-32768,32767]
int32|32位长度的整数, 取值: [-pow(2,31), pow(2,31)-1]
int64|64位长度的整数, 取值: [-pow(2,63), pow(2,63)-1]
uint8|8位无符号整数, 取值: [0,255]
uint16|16位无符号整数, 取值: [0,65535]
uint32|32位无符号整数, 取值: [0,pow(2,32)-1]
uint64|64位无符号整数, 取值: [0,pow(2,64)-1]
float16|16位半精度浮点数, 1位符号位,5位指数,10位尾数
float32|32位半精度浮点数, 1位符号位,8位指数,23位尾数
float64|64位半精度浮点数, 1位符号位,11位指数,52位尾数
complex64|复数类型,实部和虚部都是32位浮点数
complex128|复数类型,实部和虚部都是64位浮点数


#### ndarray创建方法

* 从Python中的列表、元祖等类型创建ndarray数组：
   * ` x = np.array(list/tuple/range(), dtype = np.float32)`
   * 当np.array()不指定dtype时,Numpy将根据数据情况关联一个dtype类型。
* 使用Numpy中的函数创建ndarray数组,如arange、ones、zeros等

函数|说明
:--|:---
np.arange(n)|类似range()函数,返回ndarray类型,元素从0-n-1
np.ones(shape)|根据shape生成一个全1的数组,shape是元祖类型
np.zeros(shape)|根据shape生成一个全0的数组,shape是元祖类型
np.full(shape,val)|根据shape生成一个数组,每个元素的值都是val
np.eye(n)|创建一个正方的n*n单位矩阵,对角线为1,其余为0
np.ones_like(a)|根据数组a的形状生成一个全1数组
np.zeros_like(a)|根据数组a的形状生成一个全0数组
np.full_like(a,val)|根据数组a的星创生成一个数组,每个元素值都是val
np.linspace()|根据起止数据间距地填充数据,形成数组
np.concatenate()|将两个或多个数组合并成一个新数组



举个栗子
```python
>>> a = np.linspace(1,10,4)
>>> a
array([ 1.,  4.,  7., 10.])
 
>>> b = np.linspace(1,10,4,endpoint=False)
>>> b
array([1.  , 3.25, 5.5 , 7.75])
 
>>> np.concatenate((a,b))
array([ 1.  ,  4.  ,  7.  , 10.  ,  1.  ,  3.25,  5.5 ,  7.75])
```

#### ndarray数组的维度变化

方法|说明
:--|:---
.reshape(shape)|不改变数组元素，返回一个shape形状的数组，原数组不变
.resize(shape)|与.reshape()功能一致，但改变原数组
.swapaxes(ax1,ax2)|将数组n个维度中的两个维度进行调换
.flatten()|将数组进行降维，返回折叠后的一位数组，原数组不变

栗子又来了
```python
# 不需要特别指定np.int32/np.int64 Nunpy动态识别
>>> a = np.ones((2,3,4),dtype = np.int) 
>>> a
array([[[1, 1, 1, 1],
        [1, 1, 1, 1],
        [1, 1, 1, 1]],
 
       [[1, 1, 1, 1],
        [1, 1, 1, 1],
        [1, 1, 1, 1]]])
 
>>> a.resize((3,8))
>>> a
array([[1, 1, 1, 1, 1, 1, 1, 1],
       [1, 1, 1, 1, 1, 1, 1, 1],
       [1, 1, 1, 1, 1, 1, 1, 1]])
 
>>> a.flatten()     # 原数组a没有改变 只是返回了一位数组
array([1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
       1, 1])
 
>>> b = np.ones((2,3,4),dtype = np.int)
>>> c = b.astype(np.float)
>>> c                       # 没有改变原数组b
array([[[1., 1., 1., 1.],   # c里面的元素为float 
        [1., 1., 1., 1.],
        [1., 1., 1., 1.]],

       [[1., 1., 1., 1.],
        [1., 1., 1., 1.],
        [1., 1., 1., 1.]]])
```
 
#### ndarray数组向列表转换
使用ndarray的tolist()方法  
```python
>>> a = np.full((2,3,4), 23,dtype = np.int)
>>> a
array([[[23, 23, 23, 23],
        [23, 23, 23, 23],
        [23, 23, 23, 23]],
 
       [[23, 23, 23, 23],
        [23, 23, 23, 23],
        [23, 23, 23, 23]]])
  
>>> ls = a.tolist() 
 
>>> type(ls)
<class 'list'>
  
>>> ls
[[[23, 23, 23, 23], [23, 23, 23, 23], [23, 23, 23, 23]], [[23, 23, 23, 23], [23, 23, 23, 23], [23, 23, 23, 23]]]
```

*** 
## ndarray数组的操作
#### 数组的索引和切片
* 一位数组的索引和切片：与Python的列表类似
``` python
>>> a = np.array([9,8,7,6,5,4])
>>> a[2]
7
>>> a[1:5:2]
array([8, 6])
```
 