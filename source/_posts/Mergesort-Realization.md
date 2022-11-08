---
title: Mergesort-Realization
date: 2022-11-08 22:28:52
tags:
mathjax: true
---
# 我對Mergesort的理解
--- 

因為我太菜了，所以要記錄一下現在的理解，防止以後忘記，順便讓我的文章看起來多一點。

---

mergesort是基於分治衍伸出來的排序法，基本的觀念就是把一個陣列切成多塊排序，再合併起來的排序演算法（可以想成Sort and Merge?）。

而為什麼兩個排序好得陣列合併就是排序好的呢？

$$
f(x) = \frac{x^2}{x+y}
$$