---
title: 影像處理 - 直方圖均值化 Histogram equalization
date: 2017/8/3
updated: 2017/8/3
tags:
  - tag1
  - tag2
abbrlink: 
description: 簡介
---
簡介
<!--more-->
調整圖片的對比度

**公式表達式**
$$
F(x)=(\sum_{j=0}^{size} \frac{n_j}{n})*255
$$

**基礎概念**
將分佈密集的RGB直方圖，透過機率統計的方式使直方圖分佈均勻。

統計RGB個別0~255的數值出現次數；針對出現次數以RGB數值由小到大做累積分佈函數(cdf)，並轉成0~255的數值，達成分佈均勻的目的；最後依照原圖的每個像素點，對照出新的數值。