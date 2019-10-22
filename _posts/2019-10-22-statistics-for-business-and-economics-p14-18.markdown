---
layout: post
title: "statistics-for-business-and-economics-p14-18"
date:  2019-10-22 19:30:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
The data below are the monthly salaries y and the grade point average x for
studnets who obtained a bachelor's degree in business administration with a
major in informatino system. The estimated regression equation for these data is
y = 1290.5 + 581.1x
```

GPA | Monthly Salary($)
2.6 | 2800
3.4 | 3100
3.6 | 3500
3.2 | 3000
3.5 | 3400
2.9 | 3100

```
a. Compute SST, SSR, and SSE.
b. Compute the coefficient of determination r2. Comment the goodness of fit.
c. What is the value of sample correlation coefficient?
```

## source
```python
import math
import scipy.stats
import numpy as np
import matplotlib.pyplot as plt

def query_linear_regression(x, y):
    num = len(x)
    x = np.array(x, dtype=np.float64)
    y = np.array(y, dtype=np.float64)
    xy = x * y
    xx = x * x
    yy = y * y
    print('x: ' + str(x))
    print('y: ' + str(y))
    #print('xy: ' + str(xy))
    #print('xx: ' + str(xx))
    b1 = (xy.sum() - x.sum() * y.sum() / num) / (xx.sum() - x.sum() ** 2 / num)
    b0 = y.mean() - b1 * x.mean()
    print('b0: ' + str(b0))
    print('b1: ' + str(b1))
    print('y = {0:.4f} + {1:.4f} * x'.format(b0, b1))
    SST = yy.sum() - y.sum() ** 2 / num
    SSR = ((xy.sum() - x.sum() * y.sum() / num) ** 2) / (xx.sum() - x.sum() ** 2 / num)
    SSE = SST - SSR
    r2 = SSR / SST
    r = 0
    if b1 >= 0:
        r = math.sqrt(r2)
    else:
        r = -math.sqrt(r2)
    print('SST = {0:.4f}'.format(SST))
    print('SSR = {0:.4f}'.format(SSR))
    print('SSE = {0:.4f}'.format(SSE))
    print('r2 = {0:.4f}'.format(r2))
    print('r = {0:.4f}'.format(r))

def main():
    x = [2.6, 3.4, 3.6, 3.2, 3.5, 2.9]
    y = [2800, 3100, 3500, 3000, 3400, 3100]
    query_linear_regression(x, y)

if __name__ == "__main__":
    main()
```

## output
```
x: [2.6 3.4 3.6 3.2 3.5 2.9]
y: [2800. 3100. 3500. 3000. 3400. 3100.]
b0: 1290.5405405405634
b1: 581.081081081074
y = 1290.5405 + 581.0811 * x
SST = 335000.0000
SSR = 249864.8649
SSE = 85135.1351
r2 = 0.7459
r = 0.8636
```
