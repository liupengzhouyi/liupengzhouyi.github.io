---
layout: post
title: " Optimizer"
date: 2020-02-23 20:30:00 + 0800
categories: technology
tags: tensorflow
img: https://ae03.alicdn.com/kf/Hb7f0c7d7d5844015954e4ea058d9d6710.png
---

# Optimizer

> 优化器

## 使用

```python
    with tensorflow.GradientTape() as tape:        predictions = model(images)        loss = loss_object(labels, predictions)    gradients = tape.gradient(loss, model.trainable_variables)    optimizer.apply_gradients(zip(gradients, model.trainable_variables))
```

## 方法

### `add_slot`

```
add_slot(    var,    slot_name,    initializer='zeros')
```

为添加新的广告位变量`var`。

### `add_weight`

```
add_weight(    name,    shape,    dtype=None,    initializer='zeros',    trainable=None,    synchronization=tf.VariableSynchronization.AUTO,    aggregation=tf.compat.v1.VariableAggregation.NONE)
```

### `apply_gradients`

```
apply_gradients(    grads_and_vars,    name=None)
```

将渐变应用于变量。

这是的第二部分`minimize()`。它返回一个`Operation`应用渐变的。

#### Args：

-   **`grads_and_vars`**：（梯度，变量）对的列表。
-   **`name`**：返回的操作的可选名称。默认为传递给`Optimizer`构造函数的名称。

#### Returns：

一种`Operation`适用指定梯度。的`iterations` 将被自动加1。

#### Raises：

-   **`TypeError`**：如果`grads_and_vars`格式错误。
-   **`ValueError`**：如果所有变量都不具有梯度。

### `from_config`

```
@classmethodfrom_config(    cls,    config,    custom_objects=None)
```

从其配置创建优化器。

此方法与的相反`get_config`，能够从config字典中实例化相同的优化器。

#### 参数：

-   **`config`**：Python字典，通常是get_config的输出。
-   **`custom_objects`**：将名称映射到用于创建此优化器的其他Python对象的Python字典，例如用于超参数的函数。

#### 返回值：

优化器实例。

### `get_config`

```
get_config()
```

返回优化器的配置。

优化器配置是包含优化器配置的Python字典（可序列化）。稍后可以从此配置中重新实例化同一优化器（无任何保存状态）。

#### 返回值：

Python字典。

### `get_gradients`

```
get_gradients(    loss,    params)
```

返回`loss`相对于的渐变`params`。

#### 参数：

-   **`loss`**：损失张量。
-   **`params`**：变量列表。

#### 返回值：

梯度张量列表。

#### Raises：

-   **`ValueError`**：如果无法计算任何梯度（例如，如果未实现梯度函数）。

### `get_slot`

```
get_slot(    var,    slot_name)
```

### `get_slot_names`

```
get_slot_names()
```

该优化器插槽的名称列表。

### `get_updates`

```
get_updates(    loss,    params)
```

### `get_weights`

```
get_weights()
```

### `minimize`

```
minimize(    loss,    var_list,    grad_loss=None,    name=None)
```

`loss`通过更新最小化`var_list`。

此方法仅使用[`tf.GradientTape`](https://www.tensorflow.org/api_docs/python/tf/GradientTape)和调用 来计算梯度`apply_gradients()`。如果要在应用之前处理渐变，请显式调用[`tf.GradientTape`](https://www.tensorflow.org/api_docs/python/tf/GradientTape)，`apply_gradients()`而不要使用此函数。

#### 精氨酸：

-   **`loss`**：不带参数的可调用对象，它返回的值要最小化。
-   **`var_list`**：`Variable`要更新以最小化的对象 列表或元组`loss`，或者可调用的返回`Variable`对象列表或元组。如果变量列表`minimize`在第一次`loss`调用之前已创建，则在变量列表不完整之前，请使用callable 。
-   **`grad_loss`**： 可选的。甲`Tensor`保持计算为梯度`loss`。
-   **`name`**：返回的操作的可选名称。

#### 返回值：

一`Operation`，在更新变量`var_list`。的`iterations` 将被自动加1。

#### Raises：

-   **`ValueError`**：如果某些变量不是`Variable`对象。

### `set_weights`

```
set_weights(weights)
```

### `variables`

```
variables()
```

根据创建的顺序返回此优化器的变量。