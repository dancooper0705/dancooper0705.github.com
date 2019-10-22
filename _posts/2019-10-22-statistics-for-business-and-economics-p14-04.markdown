---
layout: post
title: "statistics-for-business-and-economics-p14-04"
date:  2019-10-22 17:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
The following data were collected on the height (inches) and weight (pounds) of
women swimmers.
```

Height | 68 | 64 | 62 | 65 | 66
--- | --- | --- | --- | --- | ---
Weight | 132 | 108 | 102 | 115 | 128

```
a. Develop a scatter diagram for these data with height as the independent
variable.
b. What does the scatter diagram developed in (a) indicate about the relatipship
between the two variables?
c. Try to approximate the relationship between height and weight by drawing a
dtraight line though the data
d. Develop the estimated regression equation by computing the values of b0 and
b1 using (14.6) and (14.7).
e. If a simweer's height is 63 inches, what would you estimate her weight to be?
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
    print('x({0:.4f}) = {1:.4f}'.format(63.0, b0 + b1 * 63.0))
    estimate_x = np.linspace(x.min(), x.max(), 100, endpoint=True)
    estimate_y = b0 + estimate_x * b1
    plt.title('y = {0:.4f} + {1:.4f} * x'.format(b0, b1))
    plt.plot(x, y, 'o')
    plt.plot(estimate_x, estimate_y, '.')
    plt.show()

def main():
    x = [68, 64, 62, 65, 66]
    y = [132, 108, 102, 115, 128]
    query_linear_regression(x, y)

if __name__ == "__main__":
    main()
```

## output
```
x: [68. 64. 62. 65. 66.]
y: [132. 108. 102. 115. 128.]
b0: -240.5
b1: 5.5
y = -240.5000 + 5.5000 * x
x(63.0000) = 106.0000
```

![Figure 1](/assets/2019-10-22-statistics-for-business-and-economics-p14-04-Figure-1.png)

