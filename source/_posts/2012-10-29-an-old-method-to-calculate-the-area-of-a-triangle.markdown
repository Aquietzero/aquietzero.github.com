---
layout: post
title: "An Old Method to Calculate the Area of A Triangle"
date: 2012-10-29 13:19
comments: true
categories: [Math]
---

之前在高中的时候总结三角形面积公式的时候，碰到一个看上去比较神奇的公式：

$$
S = \sqrt{ s(s - a)(s - b)(s - c) }
$$

其中$a, b, c$分别为三角形三边边长：

$$
s = \frac{1}{2}(a + b + c)
$$

当时之所以觉得神奇是因为这个公式完全不需要三角形的角度信息，实际上三条边的长度已知就完全可以确定一个三角形，也可以通过这些边的长度来反推角度的信息，但是必要不大，因为有更为简便的方式来用这些边的长度来直接算出三角形的面积，即上面给出的公式。高中的时候只是觉得很神奇，却没有想这条公式是如何得到的，前天看书的时候再次碰到这条公式，想了一下，有下面的推导过程。

先重复描述一下问题：

> 有三角形$\triangle OAB$，其中三边长度分别为$OA = a, OB = b, AB = c$，求证其面积可以表示为$\sqrt{s(s - a)(s - b)(s - c)}$，其中$s = \frac{1}{2}(a + b + c)$。

要在没有角度信息的情况下求出三角形面积，首先想到的是用向量方法。由于两向量$\vec{A}, \vec{B}$叉乘的结果是一个与这两个向量都垂直的向量，并且其值为由这两个向量确定的平行四边形的面积。而由这两个向量所确定的三角形的面积刚好是平行四边型面积的一半，仅此，我们有：

$$
S_{\triangle{OAB}} = S = \frac{1}{2}\|\vec{A} \times \vec{B}\|
$$

根据Lagrange公式($\|\vec{A} \times \vec{B}\|^2 = \|\vec{A}\|^2 + \|\vec{B}\|^2 - (A \cdot B)^2$)，令$\vec{A} = \vec{OA}$以及$\vec{B} = \vec{OB}$，有

$$
(2S)^2 = a^2 b^2 - (\vec{A} \cdot \vec{B})^2
$$

同时，根据余弦定理，又有：

$$
c^2 = a^2 + b^2 - 2\vec{A} \cdot \vec{B}
$$

两式消去点乘项$\vec{A} \cdot \vec{B}$，有：

$$
\eqalign{
    4S^2 
    &= a^2 b^2 - \frac{1}{4}(a^2 + b^2 - c^2)^2 \\
    &= \lbrack ab + \frac{1}{2}(c^2 - a^2 - b^2) \rbrack \lbrack ab - \frac{1}{2}(c^2 - a^2 - b^2) \rbrack \\
    &= \frac{1}{4} (2ab + c^2 - a^2 - b^2)(2ab - c^2 + a^2 + b^2)
}
$$

$$
\eqalign{
    S^2
    &= \frac{1}{16} (2ab + c^2 - a^2 - b^2)(2ab - c^2 + a^2 + b^2) \\
    &= \frac{1}{16} (c^2 - (a - b)^2)((a + b)^2 - c^2) \\
    &= \frac{1}{16} (c + a - b)(c - a + b)(a + b + c)(a + b - c)
}
$$

令$s = \frac{1}{2} (a + b + c)$代入上式，即得证。
