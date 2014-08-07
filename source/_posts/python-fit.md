title: python 曲线拟合
date: 2014-03-01 09:20:24
tags: 
    - python
    - 拟合  
categories: python
---
因为工作的原因需要学习`python`, 一直用他做数据处理，主要是抓取其他程序的输出结果，然后画图，做结果分析。泽楠的论文需要用拟合的方法来处理实验数据，`origin` 算出来的结果有点奇怪，我用`matlab` 做出来的也不对，因为想试试`python`，然后结合自己写的方程求根程序，结果竟然出奇的好。下面是如何用`最小二乘法`来做`曲线拟合`。

leastsq 函数
--------------------
`python` 中有一个数值计算的包[`Scipy`](http://scipy.org),里面提供了一些数值计算的函数。其中就包括最小二乘函数`leastsq`。下面是一个简单的例子。

```python
#!/usr/bin/env python

import numpy as np
from scipy.optimize import leastsq
import pylab as pl

def fun(x, p):
	a, b = p
	return a*x + b

def residuals(p, x, y):
	return fun(x, p) - y

x1 = np.array([1, 2, 3, 4, 5, 6], dtype=float)
y1 = np.array([3, 5, 7, 9, 11, 13], dtype=float)

p0 = [1, 1]
r = leastsq(residuals, p0, args=(x1, y1))

print r[0]

pl.figure(1)
pl.plot(x1, y1, label="true data")
pl.plot(x1, fun(x1, r[0]), label="fit data")
pl.legend()
pl.show()
```
自定义的函数可以更复杂一点，`p`是需要拟合得出的系数，`p0`是这些系数的初始猜测值。
