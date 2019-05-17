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
之所以叫指数分布，是因为它的概率是指数地衰减。  
指数分布是几何分布的连续模拟，也是泊松过程中事件之间的时间的发生可能性。它和几何分布一样，具有无记忆性。也就是等待时间和已发生时间无关，比如假设灯泡是以平均速率连续且独立地发生发光或者坏了，这时我们用了灯泡的时间，假如已经用了100天了，它接下来的寿命并不会和这100天有关。（虽然实际中是有关的，因为实际中灯泡并不是以平均速率连续且独立地发生发光或者坏了。）  
指数分布是用来刻画发生某个特定事件时，所经历的时间长短的可能性。是几何分布的连续情形。  
我们回顾一下几何分布$P(X=k) = (1-p)^{k-1}p$，
对于连续情形，我们这么离散化它：我们把空间细分成$n$份，假设速率是$\lambda$，那么每一份发生特定事件的可能性$p$会满足$np = \lambda$，需要注意的是，我们离散化逼近连续情形是和泊松分布的逼近是不一样的，泊松分布的逼近是离散分布逼近离散分布，这里的是离散分布逼近连续分布，所以不能采取泊松分布那种逼近计算方式，应该要以一个分布的整体去推出连续分布。如下：  
这时，连续变量$x$可能是在第$k$个区间发生，那么$P(X=k)=(1-\frac{\lambda}{n})^{k-1}\frac{\lambda}{n}$，这里我们有$$1 = \sum_{k=1}^n P(X=k) = \sum_{k=1}^n (1-\frac{\lambda}{n})^{k-1}\frac{\lambda}{n} \rightarrow \int_0^\infty \lambda e^{-\lambda x} dx$$  
因此，概率密度函数为$f(x) = \lambda e^{-\lambda x}$， 期望为$E[X] = \frac{1}{\lambda}$， 方差为$Var[X] = \frac{1}{\lambda^2}$。

### double exponential distribution 双指数分布
双指数分布通常指的是拉普拉斯分布或者gumbel分布。拉普拉斯分布可以看成是两个指数分布的拼接。gumbel分布可以看成是两个指数函数的复合。 

#### Laplace distribution 拉普拉斯分布（双指数分布）
拉普拉斯分布的取值为$(-\infty,+\infty)$，涉及两个参数，一个是位置参数$\mu$，另一个是尺度参数$b$。概率密度函数为$f(x) = \frac{1}{2b}e^{-\frac{|x-\mu|}{b}}$。
时间上拉普拉斯运动的增量服从拉普拉斯分布。而两个iid的指数分布$X$和$Y$的差$X-Y$服从拉普拉斯分布（这个很明显，指数分布是无记忆性的，且这个差是对称的）。


#### Gumbel distribution gumbel分布（双指数分布）与广义极值分布
gumbel分布也称为广义极值分布I型，用于模拟各种分布中多个样本的极值的分布。此处，极值分布共有三种类型，具体推导可以看[极值分布的推导][extreme_value_induce]。由Fisher-Tippet-Gnedenko定理，极值的累计分布函数形如
$$G_{\xi}(\sigma x+\mu)=exp(-(1+\xi x)^{-1/\xi})$$
广义极值分布涉及三个参数，分别为位置参数$\mu$，尺度参数$\sigma$，形状参数$\xi$，其中，$\mu ,\xi \in \mathbb{R}$，$\sigma > 0$根据$\xi$的零正负三种状态，分别对应三种类型的极值分布，累计分布函数如下：
$Gumbel dist: \s F(x) = exp(-e^{\frac{x-\mu}{\sigma}}) \s \xi = 0 \s x \in \mathbb{R}$
$Frechet dist: \s F(x) = exp(-(1+\xi \frac{x-\mu}{\sigma})^{-1/\xi}) \s \xi > 0 \s x \in [\mu-\frac{\sigma}{\xi},+\infty)$
$Reversed Weibull dist: \s F(x) = exp(-(1+\xi \frac{x-\mu}{\sigma})^{-1/\xi}) \s \xi < 0 \s x \in (-\infty,\mu-\frac{\sigma}{\xi}]$
每一种极值分布类型可对应于某些分布产生的极值模型。尾部以指数下降的分布，如正态分布，其极值分布是第一类广义极值分布Gumbel分布。尾部以多项式下降的分布，如t分布，其极值分布是第二类广义极值分布。尾部有限的分布，如beta分布，其极值分布是第三类广义极值分布。  
Gumbel分布涉及两个参数$\mu$和$\sigma$，其期望为$E[X]=\mu + \gamma \sigma$，其中$\gamma$是Euler-Mascheroni常数（约等于0.5772）。方差为$Var[X]=\frac{\pi ^2}{6}\sigma^2$。  
广义极值分布可以用来表示最大值分布，可以用来对极端事件进行建模。

### normal distribution 正态分布
正态分布是非常常见且非常重要的连续型概率分布。该分布涉及两个参数，一个是位置参数$\mu$，也为该分布的期望；一个是比例参数$\sigma$，也为该分布的标准差。该分布往往记为$N(\mu,\sigma^2)$。其概率密度函数为$f(x) = \frac{1}{\sqrt{2\pi \sigma^2}}e^{-\frac{(x-\mu)^2}{2\sigma^2}}$。


### beta distribution
Beta分布的名字是因为其概率密度函数形如beta函数。该分布取值范围为$[0,1]$，该分布涉及两个参数，$\alpha$和$\beta$。概率密度函数为
$f(x) = \frac{x^{\alpha-1}(1-x)^{\beta-1}}{B(\alpha,\beta)}$，其中，$ B(\alpha,\beta) = \int_0^1 u^{\alpha-1}(1-u)^{\beta-1}du = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)}$。期望为$E[X]=\frac{\alpha}{\alpha+\beta}$，方差为$Var[X]=\frac{\alpha \beta}{(\alpha+\beta)^2(\alpha+\beta+1)}$。  
Beta分布常用于共轭先验和次序统计量中。服从于标准均匀分布$n$个样本中的第$k$最小值服从$Beta(k, n+1-k)$。

### gamma distribution
Gamma分布的名字是因为其概率密度函数形如gamma函数。该分布取值范围为$(0,+\infty)$，该分布涉及两个参数，形状参数$k$和尺度参数$\theta$，其概率密度函数为$f(x)=\frac{x^{k-1}e^{-x/\theta}}{\theta^k \Gamma(k)}$。期望为$E[X]=k\theta$，方差为$Var[X]=k\theta^2$。  
Gamma分布也用于共轭先验（如似然为泊松分布）。

### chi squared distribution
$\chi$是希腊字母，据说这个字母的来源是因为皮尔逊的手写习惯。卡方分布是这么得到的：
$Z_1,Z_2,\dots,Z_k$为服从标准正态分布的iid随机变量，它们的平方和$Q = \sum_{i=1}^k Z_i^2$服从具有$k$个自由度的卡方分布，通常表示为$Q \sim \chi^2(k)$ 或$Q \sim \chi_k^2$。卡方分布只涉及一个变量，也就是自由度$k$。卡方分布的概率密度函数为$f(x)=\frac{x^{k/2-1}e^{-x/2}}{2^{k/2} \Gamma(k/2)}$，可见卡方分布是gamma分布的特例$Gamma(k/2,2)$。卡方分布的期望为$E[X]=k$，方差为$Var[X]=2k$。卡方分布常用于卡方检验中。

### student-t distribution 
某一个版本：该分布的名称来源于William Sealy Gosset于1908年在Biometrika的笔名“学生”。Gosset 在爱尔兰都柏林的吉尼斯啤酒厂工作，并对小样品的问题感兴趣。Gosset的雇主希望他用笔名发表科学论文，因此他使用“student”这个名字来隐藏他的身份。  
t分布是这么得到的：$X_1,X_2,\dots,X_n$为服从正态分布$N(\mu,\sigma^2)$的iid随机变量，$\bar{X} = \frac{1}{n}\sum_{i=1}^n X_i$，$S^2 = \frac{1}{n-1}\sum_{i=1}^n (X_i-\bar{X})^2$，那么，$\frac{\bar{X}-\mu}{S/\sqrt{n}}$服从自由度为$n-1$的t分布。自由度为$v$的t分布的概率密度函数为：$\frac{\Gamma(\farc{v+1}{2})}{\sqrt{v\pi}\Gamma(\frac{v}{2})(1+\frac{x^2}{v})^{-\frac{v+1}{2}}} = \frac{1}{\sqrt{v}B(\frac{1}{2}(1+\frac{x^2}{v})^{-\frac{v+1}{2}},\frac{v}{2})}$，其期望为$E[X]=0 \forall v > 1$。方差为$Var[X]=\frac{v}{v-2} \forall v > 2, \infty \forall 1 < v \leq 2$，，$0 < v \leq 1$期望和方差都无定义。t分布随机变量也可以这么定义：
$T = \frac{Z}{\sqrt{V/v}}$，其中$Z \sim N(0,1)$，$V \sim \chi^2(v)$。  
随着自由度的增加，t分布接近标准正态分布，t分布的尾部比正态分布重。 t分布常用于小样本的假设检验中。


### F distribution
F分布也叫Variance Ratio Distribution（方差比分布），是以Fisher命名的。F分布涉及两个参数，都是自由度。F分布是这么得到的：
$U_1$和$U_2$分别自由度为$d_1$和$d_2$且相互独立的卡方分布。那么$X = \frac{U_1/d_1}{U_2/d_2}$服从自由度为$(d_1,d_2)$的F分布。用服从正态分布的变量构造：$S_1^2$为$d_1$个iid服从方差为$\sigma_1^2$的正态分布的随机变量的平方和，$S_2^2$为$d_2$个iid服从方差为$\sigma_2^2$的正态分布的随机变量的平方和，$X=\frac{S_1^2}{d_1 \sigma_1^2}/\frac{S_2^2}{d_2 \sigma_2^2}$为服从自由度为$(d_1,d_2)$的F分布。  
F分布的概率密度函数为$f(x)=\frac{\sqrt{\frac{(d_1 x)^{d_1}d_2^{d_2}}{(d_1 x+d_2)^{d_1+d_2}}}}{xB(\frac{d_1}{2},\frac{d_2}{2})}$。期望为$E[X]=\frac{d_2}{d_2-2} \forall d_2 > 2$，方差为$Var[X] = \frac{2d_2^2 (d_1+d_2 -2)}{d_1 (d_2-2)^2(d_2-4)} \forall d_2 > 4$。  
F分布常用于F检验等一些假设检验中。

[extreme_value_induce]:https://ckrao.wordpress.com/2012/06/10/outline-proof-of-the-extreme-value-theorem-in-statistics/
