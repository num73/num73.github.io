**原文链接**：[Newton's method for finding roots - Algorithms for Competitive Programming (cp-algorithms.com)](https://cp-algorithms.com/num_methods/roots_newton.html)

# Newton求根法

1664年Newton提出了一种迭代求根的方法。这种方法有时也被叫做Raphson方法。虽然Newton更早发现了这种方法，但Raphson首先在自己的文章中介绍了这种方法。

该方法解决的问题如下。

给定一个方程：
$$
f(x) = 0
$$
求解该方程组。更具体地来说，我们需要找到这个方程的一个根（假设这个根存在）。$f(x)$在$[a,b]$​上是可导的。

## 算法

算法的输入包括函数$f(x)$和一个初始的近似值$x_0$，这个$x_0$就是算法开始的地方。

![plot_f(x)](roots_newton.png)

假设$x_i$已知，那么需要按照接下来的方法求$x_{i+1}$。画出$f(x)$在点$x = x_i$处的切线，这条线与$x$轴的交点，这个交点的横坐标就是$x_{i+1}$，然后重复整个过程。

不难得到下面的这个等式：
$$
x_{i+1} = x_i - \frac{f(x_i)}{f^\prime(x_i)}
$$
首先，计算出$f(x)$的导数，斜率$f'(x)$，确定切线的方程为：
$$
y - f(x_i) = f'(x_i)(x_{i+1} - x_i)
$$
通过解这个方程可以得到$x_{i+1}$的值。

注意到，如果方程$f(x)$是平滑的，并且$x_i$离根足够接近，那么$x_{i+1}$与所求的根更加接近。

收敛速率是二次的。

## 求解平方根

求解平方根是应用Newton方法的一个例子。

求解$\sqrt{n}$即求方程$f(x) = x^2 - n$的根，带入上面的式子化简，可以得到
$$
x_{i+1} = \frac{x_i + \frac{n}{x_i}}{2}
$$
这个问题的第一个形式时，当$n$是一个有理数时，给定一个`eps`，可以求出它的根：

```c
double sqrt_newton(double n) {
    const double eps = 1E-15;
    double x = 1;
    for (;;) {
        double nx = (x + n / x) / 2;
        if (abs(x - nx) < eps)
            break;
        x = nx;
    }
    return x;
}
```

另一个常见的问题形式是要求求出它的整数根（给定一个$n$，求出最大的$x$使得$x^2 \leq n$）。这样的化就需要稍微改变一下这个算法的结束条件，因为当$x$开始接近答案时，可能会“跳动”。因此需要添加一个条件，如果$x$在上一次迭代中减小了，在当前的迭代中又增加了，这个时候算法必须停止。

```c
int isqrt_newton(int n) {
    int x = 1;
    bool decreased = false;
    for (;;) {
        int nx = (x + n / x) >> 1;
        if (x == nx || nx > x && decreased)
            break;
        decreased = nx < x;
        x = nx;
    }
    return x;
}
```

最后，这个问题还有一个解决非常大的数字（bignum arithmetic）的形式。由于数字$n$​可能会非常大，所以算法开始时有理由对答案进行一个初始的估计。很显然，这个估计值离答案跃进，算法收敛的越快。一般我们会选择数字$2^{bits/2}$作为这个估计值，其中$bits$是$n$的二进制位数。下面是这个问题的java实现。

```java
public static BigInteger isqrtNewton(BigInteger n) {
    BigInteger a = BigInteger.ONE.shiftLeft(n.bitLength() / 2);
    boolean p_dec = false;
    for (;;) {
        BigInteger b = n.divide(a).add(a).shiftRight(1);
        if (a.compareTo(b) == 0 || a.compareTo(b) < 0 && p_dec)
            break;
        p_dec = a.compareTo(b) > 0;
        a = b;
    }
    return a;
}
```

