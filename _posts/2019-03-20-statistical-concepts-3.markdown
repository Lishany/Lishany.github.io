---
layout: post
title:  "统计基本概念（常见连续型概率分布）"
date:   2019-03-20 21:30:00 +0800
categories: statistical-concepts
---

## 连续型概率分布
连续型概率分布是用来刻画那些取值为连续值的随机变量。期望公式的计算为：$E[X] = \int f(x)xdx$， 方差计算为 $Var[X] = E[(X-E[X])^2]$。

### uniform distribution 均匀分布
所谓均匀分布就是每个取值的可能性是一样的，均匀的，相同长度区间的取值可能性是一样的。  
该分布涉及两个参数，分别是取值最小值$a$和最大值$b$。随机变量的取值是$[a,b]$。分布通常写成$U(a,b)$，其分布密度函数为$f(x) = \frac{1}{b-a} \forall x \in [a,b]$。  
期望为$E[X] = \frac{a+b}{2}$，方差为$Var[X] = \frac{1}{12}(b-a)^2$。  
$U(0,1)$成为标准均匀分布。

### exponential distribution 指数分布
指数分布是几何分布的连续模拟，也是泊松过程中事件之间的时间的发生可能性。它和几何分布一样，具有无记忆性。也就是等待时间和已发生时间无关，比如假设灯泡是以平均速率连续且独立地发生发光或者坏了，这时我们用了灯泡的时间，假如已经用了100天了，它接下来的寿命并不会和这100天有关。（虽然实际中是有关的，因为实际中灯泡并不是以平均速率连续且独立地发生发光或者坏了。）  
指数分布是用来刻画发生某个特定事件时，所经历的时间长短的可能性。是几何分布的连续情形。  
我们回顾一下几何分布$P(X=k) = (1-p)^{k-1}p$，
对于连续情形，我们这么离散化它：我们把空间细分成$n$份，假设速率是$\lambda$，那么每一份发生特定事件的可能性$p$会满足$np = \lambda$，需要注意的是，我们离散化逼近连续情形是和泊松分布的逼近是不一样的，泊松分布的逼近是离散分布逼近离散分布，这里的是离散分布逼近连续分布，所以不能采取泊松分布那种逼近计算方式，应该要以一个分布的整体去推出连续分布。如下：  
这时，连续变量$x$可能是在第$k$个区间发生，那么$P(X=k)=(1-\frac{\lambda}{n})^{k-1}\frac{\lambda}{n}$，这里我们有$$1 = \sum_{k=1}^n P(X=k) = \sum_{k=1}^n (1-\frac{\lambda}{n})^{k-1}\frac{\lambda}{n} \rightarrow \int_0^\infty \lambda e^{-\lambda x} dx$$  
因此，概率密度函数为$f(x) = \lambda e^{-\lambda x}$， 期望为$E[X] = \frac{1}{\lambda}$， 方差为$Var[X] = \frac{1}{\lambda^2}$。

### double exponential distribution 

### normal distribution 

### beta distribution

### cauchy distribution

### chi squared distribution

### F distribution

### student distribution 

### gamma distribution

### weibull distribution


