# torch.normal()

> 返回一个张量，包含从给定参数`means`,`std`的离散正态分布中抽取随机数。 均值`means`是一个张量，包含每个输出元素相关的正态分布的均值。 `std`是一个张量，包含每个输出元素相关的正态分布的标准差。 均值和标准差的形状不须匹配，但每个张量的元素个数须相同。

## parameter

-   means (Tensor) – 均值
-   std (Tensor) – 标准差
-   out (Tensor) – 可选的输出张量

## example

```python
torch.normal(mean=0.0, std, out=None)
```

```python
torch.normal(means=torch.arange(1, 6)) 1.1681 2.8884 3.7718 2.5616 4.2500
```