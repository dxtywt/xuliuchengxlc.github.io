---
layout: post
title: 理解梯度下降
tags: mathematics
author: Liucheng Xu
disqus: y
---

* TOC
{:toc}


### 导数

导数（英语：Derivative）是微积分学中重要的基础概念。一个函数在某一点的导数描述了这个函数在这一点附近的变化率。导数的本质是通过极限的概念对函数进行局部的线性逼近。当函数f的自变量在一点x_0上产生一个增量h时，函数输出值的增量与自变量增量h的比值在h趋于0时的极限如果存在，即为f在x_0处的导数，记作f'(x_0)、\frac{\mathrm{d}f}{\mathrm{d}x}(x_0)或\left.\frac{\mathrm{d}f}{\mathrm{d}x}\right|_{x=x_0}