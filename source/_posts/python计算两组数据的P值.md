---
title: python计算两组数据的P值
date: 2020-07-10 14:35:09
tags: 数据分析, p_value
---
> 我们在做A/B试验评估的时候需要借助p_value,这篇文章记录如何利用python计算两组数据的显著性。

#### 一、代码
```python
# TTest.py
# -*- coding: utf-8 -*-
'''
# Created on 2020-05-20 20:36
# TTest.py
# @author: huiwenhua
'''

## Import the packages
import numpy as np
from scipy import stats

def get_p_value(arrA, arrB):

    a = np.array(arrA)
    b = np.array(arrB)

    t, p = stats.ttest_ind(a,b)

    return p

if __name__ == "__main__":
    get_p_value([1, 2, 3, 5, ], [6, 7, 8, 9, 10])
```

#### 二、T检验：两样本T检验
***两样本t检验***是比较两个样本所代表的两个总体均值是否存在显著差异。除了要求样本来自正态分布，还要求两个样本的总体方差相等也就是“方差齐性”。

检验原假设：样本均值无差异(μ=μ0)

Python命令stats.ttest_ind(data1,data2)

当不确定两总体方差是否相等时，应先利用levene检验检验两总体是否具有方差齐性stats.levene(data1,data2)如果返回结果的p值远大于0.05，那么我们认为两总体具有方差齐性。如果两总体不具有方差齐性，需要加上参数equal_val并设定为False，如下。

stats.ttest_ind(data1,data2,equal_var=False) // TTest中默认是具有方差齐性

#### 三、结果解释
当p值小于某个显著性水平α(比如0.05)时，则认为样本均值存在显著差异，具体的分析要看所选择的是双边假设还是单边假设（又分小于和大于）注意stats.ttest_ind进行双侧检验。   
当t值大于0，则有(（1-p）* 100)%的把握认为认为第一组数据好与第二组数据。例如p=0.05,那么我们有95%的把握认为第一组数据好于第二组数据。
