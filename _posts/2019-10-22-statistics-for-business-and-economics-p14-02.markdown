---
layout: post
title: "statistics-for-business-and-economics-p14-02"
date:  2019-10-22 15:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
Given are five observations for two variables, x and y.
```

x(i) | 2 | 3 | 5 | 1 | 8
--- | --- | --- | --- | --- | ---
y(i) | 25 | 25 | 20 | 30 | 16


```
a. Develop a scatter diagram for these data.
b. What does the  scatter diagram developed in (a) indicate about hte
relationsihp between the two variables?
c. Try to approximate the relationship between x and y and drawing a straight
line through the data.
d. Develop the estimated regression equation by computing the values of b0 and
b1 using (14.6) and (14.7).
e. Use the esitmated regression equation to predict the value of y when x = 6.
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
    print('x: ' + str(x))
    print('y: ' + str(y))
    #print('xy: ' + str(xy))
    #print('xx: ' + str(xx))
    b1 = (xy.sum() - x.sum() * y.sum() / num) / (xx.sum() - x.sum() ** 2 / num)
    b0 = y.mean() - b1 * x.mean()
    print('b0: ' + str(b0))
    print('b1: ' + str(b1))
    print('y = {0:.4f} + {1:.4f} * x'.format(b0, b1))
    print('x({0:.4f}) = {1:.4f}'.format(6.0, b0 + b1 * 6.0))
    estimate_x = np.linspace(x.min(), x.max(), 100, endpoint=True)
    estimate_y = b0 + estimate_x * b1
    plt.title('y = {0:.4f} + {1:.4f} * x'.format(b0, b1))
    plt.plot(x, y, 'o')
    plt.plot(estimate_x, estimate_y, '.')
    plt.show()

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
x(6.0000) = 19.0714
```

![Figure 1](/assets/2019-10-22-statistics-for-business-and-economics-p14-02-Figrure-1.png)

