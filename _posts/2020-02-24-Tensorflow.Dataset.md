---
layout: post
categories: posts
title: tensorflow.Dataset()
subtitle: tensorflow.Dataset()
featured-image: /images/2016-11-19/abstract-2.jpg
tags: [tensorflow]
date-string: February 24, 2020
---


# Dataset

> 数据处理

## 方法

## `__init__`

```
__init__(variant_tensor)
```

创建一个DatasetV2对象。

这是DatasetV1和DatasetV2之间的区别。DatasetV1在其构造函数中不接受任何内容，而在DatasetV2中，我们希望子类创建一个variant_tensor并将其传递给super（）调用。

#### 参数：

-   **`variant_tensor`**：表示数据集的DT_VARIANT张量。

## 物产

### `element_spec`

此数据集的元素的类型说明。

```
dataset = tf.data.Dataset.from_tensor_slices([1, 2, 3]).element_spec 
```

#### 返回值：

[`tf.TypeSpec`](https://www.tensorflow.org/api_docs/python/tf/TypeSpec)对象的嵌套结构与该数据集元素的结构相匹配，并指定各个组件的类型。

## 方法

### `__iter__`

```
__iter__()
```

创建`Iterator`用于枚举此数据集元素的。

返回的迭代器实现Python迭代器协议，因此只能在热切模式下使用。

#### 返回值：

一个`Iterator`在这个数据集的元素。

#### ### `apply`

```
apply(transformation_func)
```

将转换函数应用于此数据集。

`apply`启用自定义`Dataset`转换的链接，这些自定义转换表示为采用一个`Dataset`参数并返回transformd的函数`Dataset`。

```
dataset = tf.data.Dataset.range(100) 
```

#### 参数：

-   **`transformation_func`**：一个`Dataset`带有一个参数并返回的函数`Dataset`。

#### 返回值：

-   **`Dataset`**：`Dataset`通过应用`transformation_func`到此数据集返回。

### `as_numpy_iterator`

```
as_numpy_iterator()
```

返回一个迭代器，该迭代器将数据集的所有元素转换为numpy。

使用`as_numpy_iterator`检查你的数据集的内容。要查看元素的形状和类型，请直接打印数据集元素，而不要使用 `as_numpy_iterator`。

```
dataset = tf.data.Dataset.from_tensor_slices([1, 2, 3]) 
```

此方法要求您以渴望模式运行，并且数据集的element_spec仅包含`TensorSpec`组件。

```
dataset = tf.data.Dataset.from_tensor_slices([1, 2, 3]) 
```

```
dataset = tf.data.Dataset.from_tensor_slices([1, 2, 3]) 
```

`as_numpy_iterator()` 将保留数据集元素的嵌套结构。

```
dataset = tf.data.Dataset.from_tensor_slices({'a': ([1, 2], [3, 4]), 
```

#### 返回值：

对数据集的元素进行迭代，并将其张量转换为numpy数组。

### `batch`

```
batch(    batch_size,    drop_remainder=False)
```

将此数据集的连续元素合并为批。

```
dataset = tf.data.Dataset.range(8) 
```

```
dataset = tf.data.Dataset.range(8) 
```

生成的元素的组件将具有一个附加的外部尺寸，该尺寸将为`batch_size`（或`N % batch_size`对于最后一个元素，如果`batch_size`未将输入元素的数量`N` 平均分配`drop_remainder`为`False`）。如果您的程序依赖于具有相同外部尺寸的批次，则应将`drop_remainder` 参数设置为，`True`以防止产生较小的批次。

#### 参数：

-   **`batch_size`**：一个[`tf.int64`](https://www.tensorflow.org/api_docs/python/tf#int64)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示此数据集要在单个批次中合并的连续元素的数量。
-   **`drop_remainder`**：（可选。）一个[`tf.bool`](https://www.tensorflow.org/api_docs/python/tf#bool)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示在`batch_size`元素少于元素的情况下是否应删除最后一批 ；默认行为是不删除较小的批次。

#### 返回值：

-   **`Dataset`**：A `Dataset`。

### `cache`

```
cache(filename='')
```

在此数据集中缓存元素。

第一次迭代数据集时，其元素将缓存在指定文件或内存中。随后的迭代将使用缓存的数据。

**注意：**为了最终确定缓存，必须完整地迭代输入数据集。否则，后续迭代将不使用缓存的数据。

```
dataset = tf.data.Dataset.range(5) 
```

缓存到文件时，缓存的数据将在运行期间保持不变。即使是第一次遍历数据，也将从缓存文件中读取。`.cache()`直到删除缓存文件或更改文件名，在调用之前更改输入管道才有效。

```
dataset = tf.data.Dataset.range(5) 
```

**注意：**在整个数据集的每次迭代期间，将产生完全相同的元素。如果您希望随机化迭代顺序，请确保在调用*后再*调用。 `cache``shuffle`  `cache`

#### 参数：

-   **`filename`**：一个[`tf.string`](https://www.tensorflow.org/api_docs/python/tf#string)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示文件系统上用于在此Dataset中缓存元素的目录的名称。如果未提供文件名，则数据集将缓存在内存中。

#### 返回值：

-   **`Dataset`**：A `Dataset`。

### `concatenate`

```
concatenate(dataset)
```

`Dataset`通过将给定数据集与此数据集连接来创建一个。

```
a = tf.data.Dataset.range(1, 4)  # ==> [ 1, 2, 3 ] 
```

#### 参数：

-   **`dataset`**：`Dataset`要串联。

#### 返回值：

-   **`Dataset`**：A `Dataset`。

### `enumerate`

```
enumerate(start=0)
```

枚举此数据集的元素。

它类似于python的`enumerate`。

```
dataset = tf.data.Dataset.from_tensor_slices([1, 2, 3]) 
```

```
# The nested structure of the input dataset determines the structure of 
```

#### 参数：

-   **`start`**：一个[`tf.int64`](https://www.tensorflow.org/api_docs/python/tf#int64)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示枚举的起始值。

#### 返回值：

-   **`Dataset`**：A `Dataset`。

### `filter`

```
filter(predicate)
```

根据过滤此数据集`predicate`。

```
dataset = tf.data.Dataset.from_tensor_slices([1, 2, 3]) 
```

#### 参数：

-   **`predicate`**：将数据集元素映射到布尔值的函数。

#### 返回值：

-   **`Dataset`**：该`Dataset`包含该数据集为其中的元素 `predicate`是`True`。

### `flat_map`

```
flat_map(map_func)
```

`map_func`跨此数据集映射并展平结果。

使用`flat_map`，如果你想确保你的数据集保持不变的顺序。例如，要将批次的数据集展平为其元素的数据集：

```
dataset = Dataset.from_tensor_slices([[1, 2, 3], [4, 5, 6], [7, 8, 9]]) 
```

[`tf.data.Dataset.interleave()`](https://www.tensorflow.org/api_docs/python/tf/data/Dataset#interleave)是的推广`flat_map`，因为 `flat_map`产生的输出与 [`tf.data.Dataset.interleave(cycle_length=1)`](https://www.tensorflow.org/api_docs/python/tf/data/Dataset#interleave)

#### 参数：

-   **`map_func`**：将数据集元素映射到数据集的函数。

#### 返回值：

-   **`Dataset`**：A `Dataset`。

### `from_generator`

创建`Dataset`其元素由生成的`generator`。

所述`generator`参数必须是一个可调用的对象，返回支持的对象`iter()`协议（例如发电机功能）。生成的元素`generator`必须与给定`output_types`和（可选）`output_shapes`参数兼容 。

```
import itertools 
```

注意：[`Dataset.from_generator()`](https://www.tensorflow.org/api_docs/python/tf/data/Dataset#from_generator)使用 [`tf.numpy_function`](https://www.tensorflow.org/api_docs/python/tf/numpy_function)和的当前实现会继承相同的约束。特别是，它要求将`Dataset`和`Iterator`相关操作放在与调用Python程序相同的过程中的设备上 [`Dataset.from_generator()`](https://www.tensorflow.org/api_docs/python/tf/data/Dataset#from_generator)。的主体`generator`不会在中进行序列化`GraphDef`，并且如果您需要序列化模型并在其他环境中还原模型，则不应使用此方法。

注意：如果`generator`依赖于可变的全局变量或其他外部状态，请注意，运行时可能会调用`generator`多次（以支持重复`Dataset`），并且在[`Dataset.from_generator()`](https://www.tensorflow.org/api_docs/python/tf/data/Dataset#from_generator)从生成器调用到生成第一个元素之间的任何时间都可以调用。突变全局变量或外部状态可能导致未定义的行为，我们建议您`generator`在调用之前 显式缓存任何外部状态[`Dataset.from_generator()`](https://www.tensorflow.org/api_docs/python/tf/data/Dataset#from_generator)。

#### 参数：

-   **`generator`**：一个可调用对象，该对象返回支持`iter()`协议的对象 。如果`args`未指定，则`generator`必须不带参数；否则，它必须接受与中的值一样多的参数`args`。
-   **`output_types`**：[`tf.DType`](https://www.tensorflow.org/api_docs/python/tf/dtypes/DType)对象的嵌套结构，对应于由产生的元素的每个组成部分`generator`。
-   **`output_shapes`**：（可选。）[`tf.TensorShape`](https://www.tensorflow.org/api_docs/python/tf/TensorShape)对象的嵌套结构，对应于由产生的元素的每个组件`generator`。
-   **`args`**：（可选。）[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)将被评估并`generator`作为NumPy-array参数传递给对象的元组。

#### 返回值：

-   **`Dataset`**：A `Dataset`。

### `from_tensor_slices`

```
@staticmethodfrom_tensor_slices(tensors)
```

创建一个`Dataset`其元素为给定张量的切片的。

给定的张量沿其第一维被切片。此操作将保留输入张量的结构，删除每个张量的第一维并将其用作数据集维。所有输入张量的第一个尺寸必须相同。

```
# Slicing a 1D tensor produces scalar tensor elements. 
```

```
# Slicing a 2D tensor produces 1D tensor elements. 
```

```
# Slicing a tuple of 1D tensors produces tuple elements containing 
```

```
# Dictionary structure is also preserved. 
```

```
# Two tensors can be combined into one Dataset object. 
```

请注意，如果`tensors`包含NumPy数组，并且未启用急切执行，则值将作为一项或多项[`tf.constant`](https://www.tensorflow.org/api_docs/python/tf/constant)操作嵌入到图形中 。对于大型数据集（> 1 GB），这可能会浪费内存并遇到图序列化的字节限制。如果`tensors` 包含一个或多个大NumPy数组，请考虑[本指南中](https://tensorflow.org/guide/data#consuming_numpy_arrays)所述的替代方法。

#### 参数：

-   **`tensors`**：数据集元素，每个组件在第一维中的大小均相同。

#### 返回值：

-   **`Dataset`**：A `Dataset`。

### `from_tensors`

```
@staticmethodfrom_tensors(tensors)
```

创建一个`Dataset`包含给定张量的单个元素的。

```
dataset = tf.data.Dataset.from_tensors([1, 2, 3]) 
```

请注意，如果`tensors`包含NumPy数组，并且未启用急切执行，则值将作为一项或多项[`tf.constant`](https://www.tensorflow.org/api_docs/python/tf/constant)操作嵌入到图形中 。对于大型数据集（> 1 GB），这可能会浪费内存并遇到图序列化的字节限制。如果`tensors` 包含一个或多个大NumPy数组，请考虑[本指南中](https://tensorflow.org/guide/data#consuming_numpy_arrays)所述的替代方法。

#### 参数：

-   **`tensors`**：数据集元素。

#### 返回值：

-   **`Dataset`**：A `Dataset`。

### `interleave`

```
interleave(    map_func,    cycle_length=AUTOTUNE,    block_length=1,    num_parallel_calls=None)
```

`map_func`跨此数据集映射，并交织结果。

例如，您可以用来[`Dataset.interleave()`](https://www.tensorflow.org/api_docs/python/tf/data/Dataset#interleave)同时处理许多输入文件：

```
# Preprocess 4 files concurrently, and interleave blocks of 16 records 
```

的`cycle_length`和`block_length`参数控制在其中的元件所产生的顺序。`cycle_length`控制并发处理的输入元素的数量。如果设置`cycle_length`为1，则此转换将一次处理一个输入元素，并将产生与相同的结果[`tf.data.Dataset.flat_map`](https://www.tensorflow.org/api_docs/python/tf/data/Dataset#flat_map)。一般来说，这种转换将适用`map_func`于`cycle_length`输入元件，开放迭代对返回的`Dataset`对象，并循环通过它们产生`block_length`从每个迭代连续元素，并且每个其到达一个迭代的结束时间消耗下一个输入元件。

#### 例如：

```
dataset = Dataset.range(1, 6)  # ==> [ 1, 2, 3, 4, 5 ] 
```

注意：此变换产生的元素顺序是确定性的，只要`map_func`是纯函数即可。如果 `map_func`包含任何有状态操作，则该状态的访问顺序不确定。

#### 参数：

-   **`map_func`**：将数据集元素映射到数据集的函数。
-   **`cycle_length`**：（可选。）将同时处理的输入元素的数量。如果未指定，则将从可用的CPU内核数中得出该值。如果自`num_parallel_calls`变量设置为[`tf.data.experimental.AUTOTUNE`](https://www.tensorflow.org/api_docs/python/tf/data/experimental#AUTOTUNE)，则自`cycle_length`变量还将标识最大并行度。
-   **`block_length`**：（可选。）在循环到另一个输入元素之前，每个输入元素要生成的连续元素的数量。
-   **`num_parallel_calls`**：（可选。）如果指定，实现将创建一个线程池，该线程池用于异步和并行地从循环元素中获取输入。默认行为是从循环元素同步获取输入，而没有并行性。如果使用该值 [`tf.data.experimental.AUTOTUNE`](https://www.tensorflow.org/api_docs/python/tf/data/experimental#AUTOTUNE)，那么将根据可用的CPU动态设置并行调用的次数。

#### 返回值：

-   **`Dataset`**：A `Dataset`。

### `list_files`

```
@staticmethodlist_files(    file_pattern,    shuffle=None,    seed=None)
```

匹配一个或多个glob模式的所有文件的数据集。

该`file_pattern`参数应该是的glob模式一个小数目。如果您的文件名已被收集，请[`Dataset.from_tensor_slices(filenames)`](https://www.tensorflow.org/api_docs/python/tf/data/Dataset#from_tensor_slices)改用，因为重新使用 每个文件名`list_files`可能会导致远程存储系统性能下降。

注意：此方法的默认行为是以不确定的随机混排顺序返回文件名。传递`seed`或`shuffle=False` 以确定的顺序获取结果。

#### 例：

如果我们的文件系统上有以下文件：-/path/to/dir/a.txt-/path/to/dir/b.py-/path/to/dir/c.py如果我们传递“ / path / to / dir / *。py“作为目录，数据集将产生：-/path/to/dir/b.py-/path/to/dir/c.py

#### 参数：

-   **`file_pattern`**：一个字符串，一个字符串列表或一个[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)字符串类型（标量或向量），表示将要匹配的文件名glob（即shell通配符）模式。
-   **`shuffle`**：（可选。）如果为`True`，则文件名将随机随机排列。默认为`True`。
-   **`seed`**：（可选。）[`tf.int64`](https://www.tensorflow.org/api_docs/python/tf#int64)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示将用于创建分布的随机种子。请参阅 [`tf.compat.v1.set_random_seed`](https://www.tensorflow.org/api_docs/python/tf/compat/v1/set_random_seed)行为。

#### 返回值：

-   **`Dataset`**：`Dataset`与文件名相对应的字符串A。

### `map`

```
map(    map_func,    num_parallel_calls=None)
```

`map_func`跨此数据集的元素进行映射。

此转换适用`map_func`于此数据集的每个元素，并以与输入中出现的顺序相同的顺序返回包含转换后的元素的新数据集。`map_func`可用于更改数据集元素的值和结构。例如，向每个元素加1或投影元素组件的子集。

```
dataset = Dataset.range(1, 6)  # ==> [ 1, 2, 3, 4, 5 ] 
```

的输入签名`map_func`由此数据集中每个元素的结构确定。

```
dataset = Dataset.range(5) 
```

```
# Each element is a tuple containing two `tf.Tensor` objects. 
```

```
# Each element is a dictionary mapping strings to `tf.Tensor` objects. 
```

返回`map_func`的一个或多个值确定返回的数据集中每个元素的结构。

```
dataset = tf.data.Dataset.range(3) 
```

`map_func` 可以接受作为参数并返回任何类型的数据集元素。

请注意，无论`map_func`定义的上下文是什么（渴望与图），tf.data都会跟踪函数并将其作为图执行。要在函数内部使用Python代码，您有两个选择：

1）依靠AutoGraph将Python代码转换为等效的图形计算。这种方法的缺点是AutoGraph可以转换一些但不是全部的Python代码。

2）Use [`tf.py_function`](https://www.tensorflow.org/api_docs/python/tf/py_function)，它允许您编写任意Python代码，但通常会导致性能低于1）。例如：

```
d = tf.data.Dataset.from_tensor_slices(['hello', 'world']) 
```

#### 参数：

-   **`map_func`**：将一个数据集元素映射到另一个数据集元素的函数。
-   **`num_parallel_calls`**：（可选。）[`tf.int32`](https://www.tensorflow.org/api_docs/python/tf#int32)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示要并行异步处理的数字元素。如果未指定，则将按顺序处理元素。如果使用该值 [`tf.data.experimental.AUTOTUNE`](https://www.tensorflow.org/api_docs/python/tf/data/experimental#AUTOTUNE)，那么将根据可用的CPU动态设置并行调用的次数。

#### 返回值：

-   **`Dataset`**：A `Dataset`。

### `options`

```
options()
```

返回此数据集及其输入的选项。

#### 返回值：

甲[`tf.data.Options`](https://www.tensorflow.org/api_docs/python/tf/data/Options)表示数据集选项的对象。

### `padded_batch`

```
padded_batch(    batch_size,    padded_shapes,    padding_values=None,    drop_remainder=False)
```

将此数据集的连续元素合并为填充批次。

此转换将输入数据集的多个连续元素合并为一个元素。

像一样[`tf.data.Dataset.batch`](https://www.tensorflow.org/api_docs/python/tf/data/Dataset#batch)，结果元素的组件将具有一个附加的外部尺寸，该尺寸将为`batch_size`（或 `N % batch_size`对于最后一个元素，如果`batch_size`未将输入元素的数量`N`平均分配`drop_remainder`为`False`）。如果您的程序依赖于具有相同外部尺寸的批次，则应将`drop_remainder`参数设置为，`True`以防止产生较小的批次。

[`tf.data.Dataset.batch`](https://www.tensorflow.org/api_docs/python/tf/data/Dataset#batch)与之不同的是，要批处理的输入元素可能具有不同的形状，并且此转换会将每个组件填充为中的相应形状`padding_shapes`。该`padding_shapes`参数确定输出元素中每个组件的每个尺寸的结果形状：

-   如果尺寸是常数（例如[`tf.compat.v1.Dimension(37)`](https://www.tensorflow.org/api_docs/python/tf/compat/v1/Dimension)），则将在该尺寸中将组件填充到该长度。
-   如果尺寸未知（例如[`tf.compat.v1.Dimension(None)`](https://www.tensorflow.org/api_docs/python/tf/compat/v1/Dimension)），则组件将被填充为该尺寸中所有元素的最大长度。

```
elements = [[1, 2], 
```

另请参阅[`tf.data.experimental.dense_to_sparse_batch`](https://www.tensorflow.org/api_docs/python/tf/data/experimental/dense_to_sparse_batch)，将可能具有不同形状的元素组合为一个[`tf.SparseTensor`](https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor)。

#### 参数：

-   **`batch_size`**：一个[`tf.int64`](https://www.tensorflow.org/api_docs/python/tf#int64)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示此数据集要在单个批次中合并的连续元素的数量。
-   **`padded_shapes`**：嵌套[`tf.TensorShape`](https://www.tensorflow.org/api_docs/python/tf/TensorShape)或[`tf.int64`](https://www.tensorflow.org/api_docs/python/tf#int64)矢量张量对象的嵌套结构，表示在批处理之前应将每个输入元素的各个成分填充到的形状。任何未知的尺寸（例如[`tf.compat.v1.Dimension(None)`](https://www.tensorflow.org/api_docs/python/tf/compat/v1/Dimension)在一个 [`tf.TensorShape`](https://www.tensorflow.org/api_docs/python/tf/TensorShape)或`-1`在张量状物体）将被填充到在每个批次该维度的最大大小。
-   **`padding_values`**：（可选。）标量形的嵌套结构 [`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示要用于各个组件的填充值。默认值`0`用于数字类型，空字符串用于字符串类型。
-   **`drop_remainder`**：（可选。）一个[`tf.bool`](https://www.tensorflow.org/api_docs/python/tf#bool)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示在`batch_size`元素少于元素的情况下是否应删除最后一批 ；默认行为是不删除较小的批次。

#### 返回值：

-   **`Dataset`**：A `Dataset`。

### `prefetch`

参数

```
prefetch(buffer_size)
```

创建一个`Dataset`从该数据集中预提取元素的。

大多数数据集输入管道应以调用结束`prefetch`。这允许在处理当前元素时准备以后的元素。这通常会提高延迟和吞吐量，但以使用额外的内存存储预取元素为代价。

**注意：**与其他`Dataset`方法一样，预取对输入数据集的元素进行操作。它没有示例与批处理的概念。 `examples.prefetch(2)`将预取2个元素（2个示例），而`examples.batch(20).prefetch(2)`将预取2个元素（2个批次，每个20个示例）。

```
dataset = tf.data.Dataset.range(3) 
```

#### 参数：

-   **`buffer_size`**：一个[`tf.int64`](https://www.tensorflow.org/api_docs/python/tf#int64)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示预取时将缓冲的最大元素数。

#### 返回值：

-   **`Dataset`**：A `Dataset`。

### `range`

```
@staticmethodrange(*args)
```

创建`Dataset`逐步分隔的值范围。

```
list(Dataset.range(5).as_numpy_iterator()) 
```

#### 参数：

-   **`*args`**：遵循与python xrange相同的语义。len（args）== 1->开始= 0，停止= args [0]，step = 1 len（args）== 2->开始= args [0]，stop = args [1]，step = 1 len （args）== 3->开始= args [0]，停止= args [1，停止= args [2]

#### 返回值：

-   **`Dataset`**：A `RangeDataset`。

#### 筹款：

-   **`ValueError`**：如果len（args）== 0。

### `reduce`

```
reduce(    initial_state,    reduce_func)
```

将输入数据集简化为单个元素。

转换将`reduce_func`依次调用输入数据集的每个元素，直到数据集用完为止，以其内部状态聚合信息。该`initial_state`参数用于初始状态，并返回最终状态作为结果。

```
tf.data.Dataset.range(5).reduce(np.int64(0), lambda x, _: x + 1).numpy() 
```

#### 参数：

-   **`initial_state`**：表示转换初始状态的元素。
-   **`reduce_func`**：映射`(old_state, input_element)`到 的功能`new_state`。它必须有两个参数并返回一个新元素。的结构`new_state`必须与的结构匹配 `initial_state`。

#### 返回值：

与转换的最终状态相对应的数据集元素。

### `repeat`

```
repeat(count=None)
```

重复此数据集，以便看到每个原始值`count`。

```
dataset = tf.data.Dataset.from_tensor_slices([1, 2, 3]) 
```

注意：如果此数据集是全局状态的函数（例如，随机数生成器），则不同的重复可能会产生不同的元素。

#### 参数：

-   **`count`**：（可选。）一个[`tf.int64`](https://www.tensorflow.org/api_docs/python/tf#int64)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示应该重复数据集的次数。数据集的默认行为（如果 `count`是`None`或`-1`）是无限期重复的。

#### 返回值：

-   **`Dataset`**：A `Dataset`。

### `shard`

```
shard(    num_shards,    index)
```

创建一个`Dataset`仅包含`num_shards`此数据集1 / 的。

`shard`是确定性的。由产生的数据集`A.shard(n, i)`将包含索引为n = i的A的所有元素。

```
A = tf.data.Dataset.range(10) 
```

该数据集运算符在进行分布式培训时非常有用，因为它允许每个工作人员读取唯一的子集。

读取单个输入文件时，可以按以下方式分片元素：

```
d = tf.data.TFRecordDataset(input_file)d = d.shard(num_workers, worker_index)d = d.repeat(num_epochs)d = d.shuffle(shuffle_buffer_size)d = d.map(parser_fn, num_parallel_calls=num_map_threads)
```

#### 重要警告：

-   使用任何随机化运算符（例如随机播放）之前，请务必先进行分片。
-   通常，最好在数据集管道的早期使用分片运算符。例如，当从一组TFRecord文件读取时，在将数据集转换为输入样本之前先进行分片。这样可以避免读取每个工作程序上的每个文件。以下是完整管道中有效分片策略的示例：

```
d = Dataset.list_files(pattern)d = d.shard(num_workers, worker_index)d = d.repeat(num_epochs)d = d.shuffle(shuffle_buffer_size)d = d.interleave(tf.data.TFRecordDataset,                 cycle_length=num_readers, block_length=1)d = d.map(parser_fn, num_parallel_calls=num_map_threads)
```

#### 参数：

-   **`num_shards`**：一个[`tf.int64`](https://www.tensorflow.org/api_docs/python/tf#int64)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示并行操作的分片数。
-   **`index`**：一个[`tf.int64`](https://www.tensorflow.org/api_docs/python/tf#int64)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示worker索引。

#### 返回值：

-   **`Dataset`**：A `Dataset`。

### `shuffle`

```
shuffle(    buffer_size,    seed=None,    reshuffle_each_iteration=None)
```

随机重新排列此数据集的元素。

该数据集用`buffer_size`元素填充缓冲区，然后从该缓冲区中随机采样元素，用新元素替换所选元素。为了实现完美的改组，需要缓冲区大小大于或等于数据集的完整大小。

例如，如果您的数据集包含10,000个元素但`buffer_size`设置为1,000，则`shuffle`最初将仅从缓冲区的前1,000个元素中选择一个随机元素。选择一个元素后，其缓冲区中的空间将被下一个（即1,001个）元素替换，并保留1,000个元素的缓冲区。

`reshuffle_each_iteration`控制随机播放顺序对于每个时期是否应该不同。在TF 1.X中，创建历元的惯用方式是通过`repeat`转换：

```
dataset = tf.data.Dataset.range(3) 
```

```
dataset = tf.data.Dataset.range(3) 
```

在TF 2.0中，[`tf.data.Dataset`](https://www.tensorflow.org/api_docs/python/tf/data/Dataset)对象是Python可迭代的，这使得通过Python迭代也可以创建历元成为可能：

```
dataset = tf.data.Dataset.range(3) 
```

```
dataset = tf.data.Dataset.range(3) 
```

#### 参数：

-   **`buffer_size`**：一个[`tf.int64`](https://www.tensorflow.org/api_docs/python/tf#int64)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示此数据集中要从中采样新数据集的元素数。
-   **`seed`**：（可选。）[`tf.int64`](https://www.tensorflow.org/api_docs/python/tf#int64)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示将用于创建分布的随机种子。请参阅 [`tf.compat.v1.set_random_seed`](https://www.tensorflow.org/api_docs/python/tf/compat/v1/set_random_seed)行为。
-   **`reshuffle_each_iteration`**：（可选。）布尔值，如果为true，则表示每次迭代数据集时都应进行伪随机重排。（默认为`True`。）

#### 返回值：

-   **`Dataset`**：A `Dataset`。

### `skip`

```
skip(count)
```

创建一个`Dataset`跳过`count`此数据集中的元素的。

```
dataset = tf.data.Dataset.range(10) 
```

#### 参数：

-   **`count`**：一个[`tf.int64`](https://www.tensorflow.org/api_docs/python/tf#int64)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，代表应跳过此数据集以形成新数据集的元素数。如果`count`大于此数据集的大小，则新数据集将不包含任何元素。如果`count`为-1，则跳过整个数据集。

#### 返回值：

-   **`Dataset`**：A `Dataset`。

### `take`

```
take(count)
```

从此数据集中`Dataset`最多创建一个`count`元素。

```
dataset = tf.data.Dataset.range(10) 
```

#### 参数：

-   **`count`**：一个[`tf.int64`](https://www.tensorflow.org/api_docs/python/tf#int64)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示应构成新数据集的该数据集的元素数。如果`count`为-1，或者`count`大于此数据集的大小，则新数据集将包含此数据集的所有元素。

#### 返回值：

-   **`Dataset`**：A `Dataset`。

### `unbatch`

```
unbatch()
```

将数据集的元素拆分为多个元素。

例如，如果数据集的元素是shape `[B, a0, a1, ...]`，其中`B`每个输入元素的位置可能有所不同，那么对于数据集中的每个元素，未批处理的数据集将包含`B`shape的连续元素`[a0, a1, ...]`。

```
elements = [ [1, 2, 3], [1, 2], [1, 2, 3, 4] ] 
```

#### 返回值：

一个`Dataset`转换功能，它可以传递给 [`tf.data.Dataset.apply`](https://www.tensorflow.org/api_docs/python/tf/data/Dataset#apply)。

### `window`

```
window(    size,    shift=None,    stride=1,    drop_remainder=False)
```

将输入元素（嵌套）组合到窗口（嵌套）的数据集中。

“窗口”是大小为平面元素的有限数据集`size`（如果没有足够的输入元素来填充窗口并`drop_remainder`计算为false ，则可能会更少 ）。

所述`stride`参数确定输入元件的步幅，并且 `shift`参数确定窗口的移位。

```
dataset = tf.data.Dataset.range(7).window(2) 
```

请注意，将`window`转换应用于嵌套元素的数据集时，它将生成嵌套窗口的数据集。

```
nested = ([1, 2, 3, 4], [5, 6, 7, 8]) 
```

```
dataset = tf.data.Dataset.from_tensor_slices({'a': [1, 2, 3, 4]}) 
```

#### 参数：

-   **`size`**：一个[`tf.int64`](https://www.tensorflow.org/api_docs/python/tf#int64)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示要合并到一个窗口中的输入数据集的元素数。
-   **`shift`**：（可选。）一个[`tf.int64`](https://www.tensorflow.org/api_docs/python/tf#int64)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示每次迭代中滑动窗口的前移。默认为 `size`。
-   **`stride`**：（可选。）一个[`tf.int64`](https://www.tensorflow.org/api_docs/python/tf#int64)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示滑动窗口中输入元素的跨度。
-   **`drop_remainder`**：（可选。）[`tf.bool`](https://www.tensorflow.org/api_docs/python/tf#bool)标量[`tf.Tensor`](https://www.tensorflow.org/api_docs/python/tf/Tensor)，表示在大小小于的情况下是否应删除窗口 `window_size`。

#### 返回值：

-   **`Dataset`**：`Dataset`窗口（嵌套）中的一个-由（嵌套）输入元素创建的平面元素的有限数据集。

### `with_options`

```
with_options(options)
```

返回[`tf.data.Dataset`](https://www.tensorflow.org/api_docs/python/tf/data/Dataset)具有给定选项集的新项。

从适用于整个数据集的意义上讲，这些选项是“全局”的。如果选项设置了多次，则只要不同的选项不使用不同的非默认值，它们就会合并。

```
ds = tf.data.Dataset.range(5) 
```

#### 参数：

-   **`options`**：[`tf.data.Options`](https://www.tensorflow.org/api_docs/python/tf/data/Options)标识使用的选项。

#### 返回值：

-   **`Dataset`**：`Dataset`具有给定选项的A。

#### 筹款：

-   **`ValueError`**：将一个选项多次设置为非默认值时

### `zip`

```
@staticmethodzip(datasets)
```

`Dataset`通过将给定的数据集压缩在一起来创建一个。

此方法的语义与`zip()`Python 的内置函数相似，主要区别在于`datasets` 参数可以是`Dataset`对象的任意嵌套结构。

```
# The nested structure of the `datasets` argument determines the 
```

#### 参数：

-   **`datasets`**：数据集的嵌套结构。

#### 返回值：

-   **`Dataset`**：A `Dataset`。