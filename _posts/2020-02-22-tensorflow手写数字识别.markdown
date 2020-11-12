---
layout: post
title: " tensorflow手写数字识别"
date: 2020-02-22 20:30:00 + 0800
categories: technology
tags: tensorflow
img: https://ae03.alicdn.com/kf/Hb7f0c7d7d5844015954e4ea058d9d6710.png
---

# 手写数字识别

## 代码

```python
# 安装 TensorFlow
import tensorflow
import numpy
import matplotlib.pyplot as plt
import os
os.environ["KMP_DUPLICATE_LIB_OK"]="TRUE"

x = [0.,]
y = [0.,]

mnist = tensorflow.keras.datasets.mnist

(x_train, y_train), (x_test, y_test) = mnist.load_data()
x_train, x_test = x_train / 255.0, x_test / 255.0

model = tensorflow.keras.models.Sequential([
  # 展平输入
  tensorflow.keras.layers.Flatten(input_shape=(28, 28)),
  # 全连接层
  tensorflow.keras.layers.Dense(units=128, activation='relu'),
  # 学习率
  tensorflow.keras.layers.Dropout(0.2,),
  # 全连接层
  tensorflow.keras.layers.Dense(units=10, activation='softmax')
])

# 输出
model.summary()

model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])

# 训练
# model.fit(x_train, y_train, epochs=10)

for step in range(1, 100):
    # 在一批样品上测试模型。
    cost = model.train_on_batch(x_train, y_train, reset_metrics=False)
    x.append(float(step))
    y.append(cost[1])
    X = numpy.array(x)
    Y = numpy.array(y)
    plt.plot(X, Y, label='fitted data')
    plt.show()
    if step % 10 == 0:
        print('step: ', step, ', cost: ', cost)

# 返回测试模式下模型的损失值和指标值。
model.evaluate(x_test,  y_test, verbose=2)

```

