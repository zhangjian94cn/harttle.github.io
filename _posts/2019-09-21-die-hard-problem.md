---
title: 龙胆虎威中的四加仑水迷题（Die Hard 3）
tags: 线性组合 最大公约数 数论 离散数学
---

龙胆虎威 3 中的一个场景：在泉水旁有两个瓶子，容量分别是 5 加仑和 3 加仑。
Bruce 需要在 5 分钟内精确地得到 4 加仑水来停止定时器，差一盎司都会引起爆炸。可是用这两个瓶子总是能构造出来要求的水量吗？如果能，那么有确定的数学方法来告诉 Bruce 具体的步骤吗？

本文对这个问题进行推广，分别讨论**有解的条件**和**解的构造**两个问题，再给出判断是否有解的简单方法。有关解的存在性，我们主要证明以下两个命题：

**如果目标水量 c 能够写成 a 和 b 的线性组合就有解，否则无解**。具体地：

1. 得到的水量一定是 a 和 b 的线性组合。即如果 c 不是 a 和 b 的线性组合就无解。
2. 重复地把 a 接满倒入 b，b 满了就倒掉，a 空了就装满，就可以得到在 b（假设 b > a）中得到所有线性组合。即只要能写作线性组合就一定会得到。

**c 是否能写作 a 和 b 的线性组合，取决于 c 能否被 gcd(a,b) 整除：**

1. gcd(a,b) 是 a 和 b 最小的正的线性组合。
2. gcd(a,b) 能整除 c 等价于 c 是 a 和 b 的线性组合。

为方便讨论，本文所有线性组合都指整数线性组合，所有数字 x、y、m、n 都表示整数。

<!--more-->

## 剩余水量总是 a 和 b 的线性组合

设 a 中的水为 $V_a$，b 中的水为 $V_b$，用数学归纳法可以很容易证明 **$V_a$ 和 $V_b$ 总是 a 和 b 的线性组合**。

一、初始态两个瓶子都是空的，$V_a=V_b=0$ 是 a 和 b 的线性组合。

二、后续我们有三种操作：

0. 把其中一个倒掉。这个瓶子的水量变成 $V_a=0 \ \textrm{or} \ V_b=0$，是 a 和 b 的线性组合；另一个瓶子的水量不变。
1. 把其中一个灌满水。这个瓶子水量变成 $V_a=a \ \textrm{or} \  V_b=b$，是 a 和 b 的线性组合；另一个瓶子的水量不变。
2. 把 a 倒入 b，直到 b 满了或者 a 空了。
  * 如果 b 满了：$V'_b=b$，是 a 和 b 的线性组合；设操作前 $V_a=ra+sb, V_b=ma+nb$ 则从 a 倒出的水量 $-\Delta V_a=\Delta V_b=(1-n)b-ma$，那么 A 剩余的水量 $V'_a=(r+m)a+(s+n-1)b$，是 a 和 b 的线性组合。
  * 如果 a 空了：$V'_a=0$ 是 a 和 b 的线性组合；设操作前 $V_b=ma+nb$，则操作后 $V'_b=(m+1)a+nb$ 仍然是 a 和 b 的线性组合。

结论：$V_a$ 和 $V_b$ 总是 a 和 b 的线性组合。

## 所有 a 和 b 的线性组合都可以得到

我们给一个神奇的操作：不断地把 a 装满，倒入 b 中。如果 b 满了就都倒掉，a 倒空后再装满。它可以得到所有的线性组合。
下面来证明这一点，既然 c 是 a 和 b 的线性组合，它就可以表示为：

$$
c=ma+nb, \quad b \geq a, \quad c > 0
$$

其中：

* $b \geq a$：假设 $b$ 是大的那个瓶子，即我们总把大的那个放在右手边，最后我们会在 $b$ 中得到量为 $c$ 的水。
* $c>0$：假设我们要的水量 $c$ 是大于 $0$ 的，不然直接给空瓶子就行。

虽然我们不知道 $m$ 和 $n$ 的确切值，但我们知道存在这样的 $m$ 和 $n$。
同时，我们还可以把 $m$ 调整为正数：如果 $m$ 不是正数，就把它增加 $b$，同时 $n$ 减小 $a$ 使得上式仍然成立。
现在我们有：

$$
c=ma+nb, \quad b \geq a, \quad m>0, \quad c > 0
$$

这时 $m > 0$，而 b 中要能装得下 c，所以 $ma+nb \leq b，n \leq 1-m\frac{a}{b} < 1$，即 $n \leq 0,\quad \mid n \mid = -n$。

$$
c=\mid m \mid a- \mid n \mid b, \quad b \leq a, \quad m > 0, \quad c > 0
$$

我们在重复这一神奇操作 $\mid m \mid$ 次时，共有 $\mid m \mid a$ 的水倒入了 b。而 b 也恰好被倒掉过 $\mid n \mid$ 次：

* 如果被倒掉过 $ \mid n \mid +1$ 次，则 b 中剩余 $ \mid m \mid a- \mid n \mid b-b=c-b<0$，不可能倒成负数。
* 如果被倒掉过 $ \mid n \mid -1$ 次，则 b 中剩余 $ \mid m \mid a- \mid n \mid b+b=c+b>b$，b 中装不下。

这样在我们重复 $ \mid m \mid $ 次操作时，就得在 b 中得到了 $ \mid m \mid a- \mid n \mid b = c$ 的水。
注意我们并没有指定 c 是多少，也就是说对于任意 c，都可以通过若干次操作得到。
这就是神奇操作神奇的地方：我们不需要事先算好 $m$ 的值，只要不断地重复操作，b 中的水量为 c 时停止就好。

因此，**只要 c 是 a 和 b 的线性组合（当然必须装得下）就可以得到**。
对于龙胆虎威中 $a=3,\ b=5,\ c=4$ 的例子，$gcd(3,5)=1$，因此可以得到所有可能的水（1，2，3，4，5）。得到 $V_{b}=4$ 的操作顺序是：

第一次操作：

$V_{a}=3, V_{b}=0 \quad \rightarrow \quad V_{a}=0, V_{b}=3$

第二次操作：

$V_{b}=3, V_{b}=3 \quad \rightarrow \quad V_{a}=1, V_{b}=5 \quad \rightarrow \quad V_{a}=1, V_{b}=0 \quad \rightarrow \quad V_{a}=0, V_{b}=1$

第三次操作：

$V_{a}=3, V_{b}=1 \quad \rightarrow \quad V_{a}=0, V_{b}=4$

## gcd(a,b) 是 a 和 b 最小的正的线性组合

我们先证明一个猜想： **gcd(a,b) 是 a 和 b 最小的正的线性组合**。
即假设 $c=ma+nb$ 是 a 和 b 的最小正数组合，则 $c=gcd(a,b)$。证明思路是先证明 $c\leq gcd(a,b)$，再证明 $c \geq gcd(a,b)$。

### 1. $gcd(a,b) \leq c$

设 $G=gcd(a,b),\ a=xG,\ b=yG$，则 $c=ma+nb=(mx+ny)G$。由于 $c>0$，所以 $mx+ny \geq 1，c=(mn+ny)G \geq G$。得证。

MIT 教材中有另一种证明：因为 $gcd(a,b)  \mid  a$，且 $gcd(a,b)  \mid  b$，所以 $gcd(a,b)  \mid  ma+nb, \ for \ \forall m, n$。c 是 $ma+nb$ 的特例因此 $gcd(a,b)  \mid  c$，这意味着 $gcd(a,b) \leq c$。

### 2. $gcd(a,b) \geq c$

由于 gcd(a,b) 是最大公约数，我们通过证明 c 也是 a 和 b 的公约数，来证明 $gcd(a,b) \geq c$。
为此只需要证明 $c  \mid  a$，根据对称性可以得到 $c  \mid  b$。设 a 除以 c 的商是 x，余数是 $0 \leq y \lt c$，则：

$$
a=xc+y=x(ma+nb)+y
$$

得到 $y=(1-mx)a-nxb$，即 y 也是 a 和 b 的线性组合。由于 c 是最小的正的线性组合，所以 $y \geq c$ 或 $y \leq 0$。
由于 $y$ 是余数 $0 \leq y \lt c$，取交集 $y=0$。即 a 可以被 c 整除。得证。

## gcd(a,b) 能整除 c 等价于 c 是 a 和 b 的线性组合

这里我们要证明 a 和 b 的线性组合的集合，就是 gcd(a,b) 的倍数构成的集合。为此我们需要证明两个事情：

1. a 和 b 的线性组合都是 gcd(a,b) 的倍数
2. gcd(a,b) 的倍数是 a 和 b 的线性组合

对于1，由于 $gcd(a,b)  \mid  a，gcd(a,b)  \mid  b$，因此 $gcd(a,b)  \mid  xa+yb$，1 得证。

对于2，上一节证明了 $gcd(a,b)$ 是 a 和 b 最小的正的线性组合。
$gcd(a,b)$ 的倍数自然也是 a 和 b 的线性组合，2 得证。

**推论：目标 c 能够被 gcd(a,b) 整除就有解，否则无解。**上面几节我们证明了是否是线性组合决定了是否有解，而是否是线性组合取决于是否是 $gcd(a,b)$ 的倍数，因此：

$$
c 是否能够得到（有解）
\quad \equiv \quad
\exists m, n: c=ma+nb
\quad \equiv \quad
c \mid gcd(a,b)
$$