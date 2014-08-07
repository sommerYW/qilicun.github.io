title: python t 检验
date: 2014-03-01 09:40:32
tags: 
    - python
    - t检验
categories: python
---
同样是泽楠需要用统计方法`t检验` 来处理实验数据，虽然本科时候学过数理统计，可这都好多年过去了，早已忘干净，那时候也没用过统计的软件，据说`R`是很不错的一个统计软件，可让我现学也有点难度，于是又想起了`python` 这个万能的，易用的，语法简单的且功能强大的语言我是越来越喜欢了。于是搜索原来在`SciPy`这个包里有一些统计的函数，里面就包含最常见的`t-test`，有单样本，双样本，配对的和不配对的。统计的知识已经忘的差不多了，不多赘述，只是用例子来说明，如何用`Python` 做`t-test`


##t 检验
---------------
```python
#!/usr/bin/env python

# 1-sample t-test
from scipy import stats

data = [177.3, 182.7, 169.6, 176.3, 180.3, 179.4, 178.5, 177.2, 181.8, 176.5]

one_sample = stats.ttest_1samp(data, 175.3)

print one_sample

# unpaired t-test

x = [63.8, 56.4, 55.2, 58.5, 64.0, 51.6, 54.6, 71.0]
y = [75.5, 83.9, 75.7, 72.5, 56.2, 73.4, 67.7, 87.9]
two_sample = stats.ttest_ind(x, y)
print two_sample

two_sample_2 = stats.ttest_ind(x, y, equal_var=False)

print two_sample_2

#Paried t-test
m = [67.2, 67.4, 71.5, 77.6, 86.0, 89.1, 59.5, 81.9, 105.5]
n = [62.4, 64.6, 70.4, 62.6, 80.1, 73.2, 58.2, 71.0, 101.0]

paired_sample = stats.ttest_rel(m, n)

print paired_sample
```
