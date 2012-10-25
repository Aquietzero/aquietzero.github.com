---
layout: post
title: "The Integral Form of Factorial"
date: 2012-10-16 11:36
comments: true
categories: [Math]
---

最近在复习概率，在看到Stirling公式的时候，顺便看到了阶乘的积分形式，在此记录一下。

## 阶乘定义

我们最初接触阶乘的时候估计是使用如下定义：

$$
f(n) =
\begin{cases}
    0         & , n = 0 \\
    nf(n - 1) & , n > 0 \\
\end{cases}
$$

## 阶乘积分定义

如果要寻找该公式对应的积分，那必须满足一下的条件（假设该积分为$F(n)$）：

1. 当$n = 0$，$F(n) = 0! = 1$。
2. 当$n \in \Bbb Z$，$F(n) = n!$。
3. 当$n \notin \Bbb Z$，有$(\lfloor n \rfloor - 1)! < F(n) < \lceil n \rceil !$。

为了满足上述条件，考虑下面的函数：

$$
    F(n) = \int_x^{\infty} x^n e^{-x} \mathrm{d}x
$$

用分部积分，有：

$$
\begin{align}
    \int_0^{\infty} x^n e^{-x} \mathrm{d}x 
        &= \lim_{x \to \infty} -x^n e^{-x} - n \int_0^{\infty} x^{n-1} e^{-x} \mathrm{d}x \\
        &= nF(n - 1)
\end{align}
$$

由此满足了其递归的定义，既然满足了递归的定义，那么当$n \in \Bbb Z$的时候，必然满足上面的条件2。根据函数图像，条件3也能够验证。对于第一点条件，有当$n = 0$的时候，我们有

$$
\begin{align}
    \int_0^{\infty} x^n e^{-x} \mathrm{d}x 
        &= \int_0^{\infty} e^{-x} \mathrm{d}x \\
        &= -\lim_{x \to \infty} e^{-x} + e^0 = 1
\end{align}
$$

所以上述定义的函数$F(n)$确实是可以作为阶乘的积分定义的。

## 非整数阶乘

有了阶乘的积分定义以后，计算阶乘的时候就没有必要要求是整数了。比如计算$4.5!$，根据其阶乘的递归定义，我们有

$$
\begin{align}
4.5! 
    &= 4.5 \times F(4.5 - 1) \\
    &= 4.5 \times 3.5 \times F(3.5 - 1) \\
    &= 4.5 \times 3.5 \times 2.5 \times F(2.5 - 1) \\
    &= 4.5 \times 3.5 \times 2.5 \times 1.5 \times F(1.5 - 1) \\
    &= 4.5 \times 3.5 \times 2.5 \times 1.5 \times F(0.5)
\end{align}
$$

于是我们需要计算的就仅仅只有最后一项$F(0.5)$了。将其代入积分，同样使用分部积分法，我们有：

$$
\begin{align}
    \int_0^{\infty} \sqrt{x} e^{-x} \mathrm{d}x 
        &= 2 \int_0^{\infty} y^2 e^{-y^2} \mathrm{d}y \\ 
        &= -\lim_{y \to \infty} y e^{-y^2} - \int_0^{\infty} e^{-y^2} \mathrm{d}y \\
        &= \frac{\sqrt{\pi}}{2}
\end{align}
$$

于是：

$$
F(4.5) = 4.5 \times 3.5 \times 2.5 \times 1.5 \times \frac{\sqrt{\pi}}{2}
$$
