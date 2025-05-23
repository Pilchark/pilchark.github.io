---
title: 归并排序复杂度分析
description: Complexity Analysis of Merge Sort
date: 2025-03-12
categories:
    - Development
tags:
---

归并排序复杂度分析

> 归并排序(Mergesort)复杂度分析中处理向上取整⌈n/2⌉和向下取整⌊n/2⌋的问题。

## 核心问题

在实际中,归并排序的递归关系是:
```
T(n) = T(⌈n/2⌉) + T(⌊n/2⌋) + O(n)
```

这比理想化的递归式 T(n) = 2T(n/2) + O(n) 要复杂,因为当n为奇数时,子问题大小不均等。

## 解决方法:域变换(Domain Transformation)

1. **放宽上界**:
   - 我们用更大的值来估计: T(n) ≤ 2T(⌈n/2⌉) + n ≤ 2T(n/2 + 1) + n

2. **引入新函数**:
   - 定义 S(n) = T(n + α),选择适当的α使S(n)满足更简单的递归式

3. **推导S(n)的递归关系**:
   - S(n) = T(n+α)
   - ≤ 2T(n/2+α/2+1) + n+α
   - = 2S(n/2−α/2+1) + n+α

4. **选择α = 2**:
   - 这使递归式简化为 S(n) ≤ 2S(n/2) + n + 2
   - 现在可以用递归树方法得出 S(n) = O(n log n)
      T(n) = S(n-2) =  O((n−2)log(n−2)) = O(nlogn)

## 总结

想象一下这个问题:
- 当我们把问题分成两半时,由于整除问题,可能会导致一半略大,一半略小
- 这会让数学分析变得复杂
- 通过"域变换"技巧,我们可以将问题转化为更整洁的形式
- 本质是:通过定义一个稍微调整了输入大小的新函数,使递归式更容易分析

重要结论:在大多数情况下,向上取整和向下取整对最终的渐近复杂度没有影响,可以在分析时忽略这些细节。


参考：
  - < Algorithm-Jeffe> p53
