---
layout: post
categories: posts
title: numpy.array
subtitle: Numpy.Array方法
featured-image: /images/2016-11-19/abstract-4.jpg
tags: [numpy]
date-string: February 20, 2020
---

# Numpy.Array

> 通常，可以通过使用array（）函数将Python中以数组状结构排列的数值数据转换为数组。
> 最明显的例子是列表和元组。
> 有关使用的详细信息，请参见array（）的文档。
> 一些对象可能支持数组协议，并允许以这种方式转换为数组。
> 确定是否可以使用array（）将对象转换为numpy数组的一种简单方法
> 是以交互方式尝试并查看其是否有效！（Python方式）。

## array()

```python
x = np.array([2,3,1,0])
x = np.array([2, 3, 1, 0])
x = np.array([[1,2.0],[0,0],(1+1j,3.)])
x = np.array([[ 1.+0.j, 2.+0.j], [ 0.+0.j, 0.+0.j], [ 1.+1.j, 3.+0.j]])
```

