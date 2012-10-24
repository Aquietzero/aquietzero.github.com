---
layout: post
title: "Vector Space of Complex N-tuple"
date: 2012-10-23 20:23
comments: true
categories: [Math]
---

向量空间$\Bbb R^n$实际上可以扩充到复数域，从而推广到复数向量空间$\Bbb C^n$。与$\Bbb R^n$类似，对于$\Bbb C^n$我们有

$$
\vec{A} = \vec{B} \Leftrightarrow i = 1, 2, \cdots, n, a_i = b_i, \\
\vec{A} + \vec{B} = (a_1 + b_1, \cdots, a_n + b_n), \\
c\vec{A} = (ca_1, \cdots, ca_n).
$$

其中上面的常量$a_i, b_i, c$都是复数，由此我们得到了**复n维空间**，记为$\Bbb C^n$。

有很多关于$\Bbb R^n$的定理都可以原封不动地移植到$\Bbb C^n$上，不过与点积有关的定理仍需要进行修正，我们用不全为0的实数的平方和为正这一事实来证明非零向量与自己的点积为正，**由于复数的平方和有可能为负，为了保留正定性，我们必须修改点积的定义。**


## 复n维空间的点积定义

设$\vec{A} = (a\_1, \cdots, a\_n), \vec{B} = (b\_1, \cdots, b\_n)$为$\Bbb C^n$中的两个向量，我们用如下的公式来定义它们的点积$\vec{A} \cdot \vec{B}$：

$$
\vec{A} \cdot \vec{B} = \sum^n_{k=1} a_k \overline{b_k} 
$$

其中$\overline{b_k}$是$b_k$的共轭复数。

根据这样的定义，就有一些定理需要修正了，比如：

$$
\vec{A} \cdot \vec{B} = \overline{ \vec{B} \cdot \vec{A} }, \\
c(\vec{A} \cdot \vec{B}) = (c \vec{A}) \cdot \vec{B} = \vec{A} \cdot (\overline{c} \vec{B}).
$$

这些都是显而易见的推广，在此就不证明了。

## 一些例子

**1. 证明：对$\Bbb C^n$中任意两个向量$\vec{A}$和$\vec{B}$，有恒等式**

$$
\| \vec{A} + \vec{B} \|^2 = 
    \| \vec{A} \|^2 + \| \vec{B} \|^2 + 
    \vec{A} \cdot \vec{B} + 
    \overline{ \vec{A} \cdot \vec{B} }
$$

证：令$\vec{C} = \vec{A} + \vec{B}$，于是有

$$
\eqalign{
    \| \vec{A} + \vec{B} \|^2 
    &= \|\vec{C}\| \cdot \|\vec{C}\| \\
    &= \sum^n_{k=1} c_k \overline{c_k} \\
    &= \sum^n_{k=1} (a_k + b_k)(\overline{a_k} + \overline{b_k}) \\
    &= \sum^n_{k=1} (a_k \overline{a_k} + a_k \overline{b_k} + b_k \overline{a_k} + b_k \overline{b_k}) \\
    &= \|\vec{A}\|^2 + \|\vec{B}\|^2 + \vec{A} \cdot \vec{B} + \vec{B} \cdot \vec{A} \\
    &= \|\vec{A}\|^2 + \|\vec{B}\|^2 + \vec{A} \cdot \vec{B} + \overline{\vec{A} \cdot \vec{B}}
}
$$

**2. 证明：对于$\Bbb C^n$中的任意两个向量$\vec{A}$和$\vec{B}$，$\vec{A} \cdot \vec{B} + \overline{\vec{A} \cdot \vec{B}}$是实数。**

证：由定义有

$$
\vec{A} \cdot \vec{B} + \overline{\vec{A} \cdot \vec{B}} = \sum^n_{k=1} (a_k \overline{b_k} + \overline{a_k} b_k)
$$

令$a\_k = x\_{ak} + y\_{ak} \jmath, b\_k = x\_{bk} + y\_{bk} \jmath$，代入上式，即可算得其虚部系数为0，所以上式的结果必然是实数。 

## 复n维空间的夹角问题

为了对夹角公式进行修正，在复n维空间中，两个向量之间的夹角有如下定义：

$$
\cos \theta = \frac{\vec{A} \cdot \vec{B} + \overline{\vec{A} \cdot \vec{B}}}{2\|\vec{A}\|\|\vec{B}\|}
$$

当然，这样定义的原因之一在于，上式右端的值域符合$\cos \theta$的值域，再有则是根据$\Bbb R^n$上的公式$\cos \theta = \frac{\vec{A} \cdot \vec{B}}{\|\vec{A}\|\|\vec{B}\|}$变形而来，下面简单证明一下值域相等的问题。

由Cauchy-Schwarz不等式有

$$
| \vec{A} \cdot \vec{B} |^2 \leq (\vec{A} \cdot \vec{A})(\vec{B} \cdot \vec{B})
$$

对其两端开方，有

$$
-\|\vec{A}\|\|\vec{B}\| \leq 
\vec{A} \cdot \vec{B} \leq 
\|\vec{A}\|\|\vec{B}\|
$$

同理，有$\vec{B} \cdot \vec{A} = \overline{\vec{A} \cdot \vec{B}}$

$$
-\|\vec{A}\|\|\vec{B}\| \leq 
\overline{\vec{A} \cdot \vec{B}} \leq 
\|\vec{A}\|\|\vec{B}\|
$$

两式相加即可证得其值域为$\lbrack -1, 1 \rbrack$。
