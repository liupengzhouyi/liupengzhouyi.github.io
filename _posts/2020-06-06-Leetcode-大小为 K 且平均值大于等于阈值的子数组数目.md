---
layout: post
title: Leetcode - 大小为 K 且平均值大于等于阈值的子数组数目
date: 2020-06-06 20:30:00 + 0800
subtitle: Leetcode - 大小为 K 且平均值大于等于阈值的子数组数目
categories: posts
tags: [leetcode]
img: https://ooo.0o0.ooo/2017/05/27/5929398cad637.jpg
---

# [大小为 K 且平均值大于等于阈值的子数组数目](https://leetcode-cn.com/problems/number-of-sub-arrays-of-size-k-and-average-greater-than-or-equal-to-threshold/)

## Title:



![截屏2020-06-06 下午4.28.55](https://tva1.sinaimg.cn/large/007S8ZIlly1gfing49luzj310c0n8adn.jpg)

## My Code

```C++
int ArrayNumbers::numOfSubarrays(std::vector<int> &arr, int k, int threshold) {
    auto arrayNumbers = 0;
    auto sum = 0;
    for (int i = 0; i < k; i++) sum = sum + arr[i];
    for (int i = k; i < arr.size(); i++) {
        if (sum/k >= threshold) arrayNumbers = arrayNumbers + 1;
        sum = sum + arr[i];
        sum = sum - arr[i - k];
    }
    if (sum/k >= threshold) arrayNumbers = arrayNumbers + 1;
    return arrayNumbers;
}
```



## Result

![截屏2020-06-06 下午4.30.19](https://tva1.sinaimg.cn/large/007S8ZIlly1gfinhjo0hdj30y40a4wfn.jpg)

