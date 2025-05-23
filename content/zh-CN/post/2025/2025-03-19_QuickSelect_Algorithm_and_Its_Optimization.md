---
title: QuickSelect 算法及其优化
description: QuickSelect_Algorithm_and_Its_Optimization
date: 2025-03-19
categories:
    - Development
tags:
---

# QuickSelect QuickSelect 算法及其优化

QuickSelect 是一个寻找数组中第 k 小元素的算法。这段内容主要介绍了 QuickSelect 算法及其优化版本 MomSelect 算法。

## 基本 QuickSelect 算法

1. **原理**：选择一个枢轴元素(pivot)，将数组分成两部分，然后只在包含第 k 小元素的那部分继续搜索。
2. **特点**：
   - 与 QuickSort 使用相同的分区子程序
   - 算法正确性不依赖于枢轴的选择方式
   - 需要解决一般性的选择问题，而不仅仅是中位数

## 复杂度分析

### 最坏情况

如果每次选择的枢轴都是最小或最大元素，递归式为：
```
T(n) = T(n-1) + O(n)
```
解得 T(n) = O(n²)

### 好的枢轴情况

如果能选择接近中位数的枢轴，使得每次递归处理的子问题大小不超过 αn（α < 1），递归式为：
```
T(n) ≤ T(αn) + O(n)
```
解得 T(n) = O(n)

## MomSelect 算法（中位数的中位数）

为了确保获得好的枢轴，MomSelect 算法：

1. 将数组分成每组5个元素的块
2. 暴力计算每个块的中位数
3. 递归计算这些中位数的中位数（即"中位数的中位数"）作为枢轴
4. 用这个枢轴进行分区并递归搜索相应的一侧

这个算法确保了每次分区后，至少有约 30% 的元素会被排除，从而保证了 O(n) 的线性时间复杂度。

## 为什么是 30%(3/10)?

这段文字描述了一种算法的可视化方法，主要解释了"中位数的中位数"(median-of-medians)算法的工作原理：

1. 将输入数组想象为一个5×⌈n/5⌉的网格，每列代表连续的5个元素。
2. 假设我们对每列元素从上到下排序，然后按中间元素对列排序（注意：算法实际上不执行此排序）。
3. 在这种排列中，中位数的中位数(mom)是最接近网格中心的元素。
4. 如果我们寻找的元素大于mom，算法会丢弃所有小于mom的元素，包括网格前三行左半部分的3n/10个元素。
5. 类似地，如果目标元素小于mom，算法会丢弃至少3n/10个大于mom的元素。
6. 因此，递归子问题的输入规模至多为原问题的7n/10。

该算法通过这种"中位数的中位数"方法确保每次递归都能显著减小问题规模。

参考：
  - < Algorithm-Jeffe> p53
