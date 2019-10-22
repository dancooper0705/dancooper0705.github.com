---
layout: post
title: "statistics-for-business-and-economics-p14-16"
date:  2019-10-22 19:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
The data from Exercies2 follow
```

x(i) | 2 | 3 | 5 | 1 | 8
--- | --- | --- | --- | --- | ---
y(i) | 25 | 25 | 20 | 30 | 16


```
The estimated regression equation for these data is y = 30.33 - 1.88x.
a. Compute SSE, SST, and SSR
b. Compute the coefficient of determination r^2. Comment on the goodness of fit.
c. Compute the sample correlation coefficient.
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
    x = [2, 3, 5, 1, 8]
    y = [25, 25, 20, 30, 16]
    query_linear_regression(x, y)

if __name__ == "__main__":
    main()
```

## output
```
x: [2. 3. 5. 1. 8.]
y: [25. 25. 20. 30. 16.]
b0: 30.33116883116883
b1: -1.876623376623377
y = 30.3312 + -1.8766 * x
SST = 114.8000
SSR = 108.4688
SSE = 6.3312
r2 = 0.9449
r = -0.9720
```
