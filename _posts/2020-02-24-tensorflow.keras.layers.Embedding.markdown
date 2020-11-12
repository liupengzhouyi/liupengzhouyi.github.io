---
layout: post
title: " tensorflow.keras.layers.Embedding"
date: 2020-02-24 20:30:00 + 0800
categories: technology
tags: [tensorflow]
img: https://ae03.alicdn.com/kf/Hb7f0c7d7d5844015954e4ea058d9d6710.png
---

# tensorflow.keras.layers.Embedding

> 将正整数（索引）转换为固定大小的密集向量。

### 例如

`[[4], [20]] -> [[0.25, 0.1], [0.6, -0.2]]`

该层只能用作模型中的第一层。

## 使用

```python
model.add(tensorflow.keras.layers.Embedding(10000, 16))
# 10000词汇量,每个词用16位向量表示
```

#### 参数：

-   **`input_dim`**：int>0。词汇表的大小，即最大整数索引+ 1。
-   **`output_dim`**：int> =0。密集嵌入的尺寸。
-   **`embeddings_initializer`**：`embeddings`矩阵的初始化器。
-   **`embeddings_regularizer`**：正则化函数应用于`embeddings`矩阵。
-   **`embeddings_constraint`**：约束函数应用于`embeddings`矩阵。
-   **`mask_zero`**：输入值0是否为应屏蔽的特殊“填充”值。这在使用可能需要可变长度输入的循环图层时很有用。如果是这样，`True`则该模型中的所有后续层都需要支持屏蔽，否则将引发异常。结果，如果mask_zero设置为True，则无法在词汇表中使用索引0（input_dim应等于词汇表大小+ 1）。
-   **`input_length`**：输入序列的长度（恒定时）。如果要连接`Flatten`然后在`Dense`上游连接图层，则需要此参数 （否则，将无法计算密集输出的形状）。

#### 输入形状：

形状为的2D张量：`(batch_size, input_length)`。

#### 输出形状：

形状为的3D张量：`(batch_size, input_length, output_dim)`。

## exmaple

```python
model = Sequential()
model.add(Embedding(input_dim=1000, output_dim=64, input_length=10))
# 1000词汇量，每个句子10长度，每个词用64位向量表示
```

最大的整数（输入中的单词索引不应大于999）。

model.output_shape=（None，10，64），其中None是批处理维度。