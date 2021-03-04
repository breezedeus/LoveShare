---
marp: true
_class: lead
paginate: true
backgroundColor: #fff
---
<style>
h1 {
  font-size: 60px;
  color: #09c;
}
section.split {
    overflow: visible;
    display: grid;
    grid-template-columns: 500px 500px;
    grid-template-rows: 100px auto;
    grid-template-areas: 
        "slideheading slideheading"
        "leftpanel rightpanel";
}
/* debug */
section.split h3, 
section.split .ldiv, 
section.split .rdiv { border: 0pt dashed dimgray; }
section.split h3 {
    grid-area: slideheading;
    font-size: 50px;
}
section.split .ldiv { grid-area: leftpanel; }
section.split .rdiv { grid-area: rightpanel; }
</style>
</style>

<!-- _paginate: false -->

# 充分统计量与指数族分布

何元珍
2021-03-04

---
# 充分统计量（Sufficient Statistics）

* **统计量** $T=T(X)$ 是样本的函数，它是对样本 $X$ 的“加工”或压缩
* 通俗理解：
  $$\begin{aligned}\{X \text{ 所包含的关于参数 }\theta \text{ 的信息}\} =& \{\ T(X) \text{ 所包含的关于参数 }\theta \text{ 的信息}\} \\ & + \{\text{已知 } T(X) \text{ 后，} X \text{ 还包含的关于参数 } \theta \text{ 的信息}\} \end{aligned}
  $$
* 若后一项为零，则称 $T(X)$ 是**充分统计量**
  * 已知 $T(X)$ 后，此时 $X$ 的条件分布不再与 $\theta$ 有关


---
# 充分统计量（Sufficient Statistics）

**充分统计量** 定义：给定 $X \sim\left(\mathbb{X}, \mathcal{B} X, P^{X} \theta\right),\ \theta \in \Theta,\  T(X)$ 称为**充分统计量**，若条件概率 $P_{\theta}^{X}(A \mid T(X)=t) \stackrel{d}{=} P_{\theta}^{X}(A \mid t)$ 与 $\theta$ 无关，即条件分布 $F(x \mid t, \theta)$ 或条件密度 $f(x \mid t ; \theta)$ 与 $\theta$ 无关

**因子分解定理（Fisher–Neyman Factorization theorem）**：设总体概率函数为 $f(x ; \theta),\ x_{1}, \ldots, x_{n}$ 为样本，那么 $T=T\left(x_{1}, \ldots, x_{n}\right)$ 为充分统计量的**充要条件**为：存在函数 $g(t, \theta)$ 与 $h\left(x_{1}, \ldots, x_{n}\right)$，使得对任意的 $\theta$ 和任意一组的观测值 $\left(x_{1}, \ldots, x_{n}\right)$， 都有：

$$f\left(x_{1}, \cdots, x_{n} ; \theta\right)=g\left(T\left(x_{1}, \cdots, x_{n}\right), \ \theta\right) h\left(x_{1}, \cdots, x_{n}\right)$$

---
# 充分统计量（Sufficient Statistics）
## 示例 1

设 $x_{1}, \cdots, x_{n}$ 为来自 $p(x ; \theta)=\theta x^{\theta-1}, \ 0<x<1,\ \theta>0$ 的样本，求出它的一个充分统计量。

首先，求出其联合概率密度：

$$p\left(x_{1}, \cdots, x_{n}, \theta\right)=\theta^{n}\left(\prod_{i=1}^{n} x_{i}\right)^{\theta-1}$$

取：
* $g(t, \theta) = \theta^{n}t^{\theta-1}$，$h\left(x_{1}, x_{2}, \cdots, x_{n}\right)=1$

可得**充分统计量 $T=\prod_{i=1}^{n} x_{i}$**

---
# 充分统计量（Sufficient Statistics）
## 示例 2
设 $x_{1}, \cdots, x_{n}$ 独立同分布，并且 $x_{i} \sim p\left(x_{i} ; \mu, \sigma^{2}\right)=\frac{1}{\sqrt{2 \pi} \sigma x_{1}} \exp \left\{-\frac{1}{2 \sigma^{2}}\left(\ln x_{i}-\mu\right)^{2}\right\}$ 的充分统计量。

其联合密度函数：

$$\begin{aligned} p\left(x_{1}, \cdots, x_{n} ;\ \mu, \sigma^{2}\right)&=\prod_{i=1}^{n} \frac{1}{\sqrt{2 \pi} \sigma x_{i}} \exp \left\{-\frac{1}{2 \sigma^{2}} \sum_{i=1}^{n}\left(\ln x_{i}-\mu\right)^{2}\right\} \\ &=\prod_{i=1}^{n} \frac{1}{\sqrt{2 \pi} x_{i}} \sigma^{-n} \exp \left\{-\frac{1}{2 \sigma^{2}} \sum_{i=1}^{n} \ln ^{2} x_{i}+\frac{\mu}{\sigma^{2}} \sum_{i=1}^{n} \ln x_{i}-\frac{n \mu^{2}}{2 \sigma^{2}}\right\} \end{aligned}$$

* 只要让 $h(x_{1}, x_{2}, \cdots, x_{n})=\prod_{i=1}^{n} \frac{1}{\sqrt{2 \pi} x_{i}}$，其他项都放到函数 $g(T, \theta)$ 中即可

---
# 充分统计量（Sufficient Statistics）
## 示例 2
可见以下统计量即为**充分**的：

$$T=\left(\sum_{i=1}^{n} \ln ^{2} x_{i},\ \sum_{i=1}^{n} \ln x_{i}\right)$$


> 一般情况下，$n$ 个统计量解决 $n$ 个未知参数。

---
# 指数族分布
## 指数族分布的定义

如果概率密度函数 $f(x ; \theta)$ 可以写成

$$f(x ; \theta)=c(\theta) \exp \left\{\sum_{j=1}^{k} c_{j}(\theta) T_{j}(x)\right\} h(x) $$

* 其中 $c(\theta),\ c_{j}(\theta)$ 不含 $x$，（ $c(\theta),\ c_{j}(\theta)$ 是不同的项，后者*不是* 前者的分量）, $T_{j}(x),\ h(x)$ 不含 $\theta$ 。分布的支撑 $\{x \mid f(x ; \theta)>0\}$ 不依赖于参数 $\theta$（所以均匀分布不是指数族分布）

---
# 指数族分布
## 指数族分布的标准形式

* 可以令 $w_{j}=c_{j}(\theta),\ j=1, \ldots, k$ 解出 $\theta=\theta\left(w_{1}, \ldots, w_{k}\right)$，从而 $c(\theta)=c(\theta(w))=c^{*}(w)$
* 即 $c(\theta),\ c_{j}(\theta)$ 均用 $\left(w_{1}, \ldots, w_{k}\right)$ 向量表示，代回密度函数得到指数族的标准形式：

$$f(x ; \theta)=c^{*}(w) \exp \left\{\sum_{j=1}^{k} w_{j} T_{j}(x)\right\} h(x)
$$

> 大部分常用分布都是指数族分布。

---
# 指数族分布
## 示例1：二项分布

$$P_{\theta}(x)=\binom{n}{x} \theta^{x}(1-\theta)^{n-x}=\binom{n}{x}(1-\theta)^{n} \exp \left\{x \ln \frac{\theta}{1-\theta}\right\}$$

---
# 指数族分布
## 示例2：正态分布

$$\begin{aligned}P_{\theta}(x)&=\frac{1}{\sqrt{2 \pi} \sigma} e^{-\frac{(x-\mu)^{2}}{2 \sigma^{2}}}=\left[\frac{1}{\sqrt{2 \pi} \sigma} e^{-\frac{\mu^{2}}{2 \sigma^{2}}}\right] e^{-\frac{x^{2}}{2 \sigma^{2}}+\frac{\mu}{\sigma^{2}} x} \\ &=c(\mu, \sigma) \exp \left\{c_{1}(\mu, \sigma) x+c_{2}(\mu, \sigma) x^{2}\right\}\end{aligned}$$

其中 $T_{1}(x)=x,\ T_{2}(x)=x^{2},\ h(x)=1$ 。


> 指数族分布有一些很好的特性，例如必定存在共轭先验分布等。

<!--

---
# 参考资料

- [数理统计|笔记整理（3）——充分统计量](https://zhuanlan.zhihu.com/p/87520809)
- [高等数理统计—第二章 充分统计量、完备性、样本信息](https://zhuanlan.zhihu.com/p/91053206)
- [Sufficient statistic - Wikipedia](https://en.wikipedia.org/wiki/Sufficient_statistic)
- [03 统计学基础--指数族和充分完备统计量](https://www.slidestalk.com/u198/mathematics_statistics_03)
- [指数族分布](https://zhuanlan.zhihu.com/p/66777539)

-->