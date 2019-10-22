---
layout: post
title: "statistics-for-business-and-economics-p14-06"
date:  2019-10-22 17:30:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
Airline performance data for U.S. airlines where reported in the wall Street
Journal Almanac 1998. Data on the percentage of flights arriving on time and the
number of complaints per 100,000 passengers follow.
```

Airline | Percentage on Time | Complaints
--- | --- | ---
Southwest | 81.8 | 0.21
Continental | 76.6 | 0.58
Northwest | 76.6 | 0.85
US Airways | 75.7 | 0.68
United | 73.8 | 0.74
American | 72.2 | 0.93
Delta | 71.2 | 0.72
America West | 70.8 | 1.22
TWA | 68.5 | 1.25


```
a. Develop a scatter diagram for these data.
b. What does the scatter diagram developed in (a) indicate about the
relationship between the two variables?
c. Develop the estimated regression equation showing how the percentage of
flights arriving on time is related to the number of complaints per 100,000
passengers.
d. Provide an interpretatino for the slope of the estimated regression equation.
e. What is the estimated number of complaints per 100,000 passengers if the
percentage of flights arriving on time is 80%?
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
    print('x({0:.4f}) = {1:.4f}'.format(80.0, b0 + b1 * 80.0))
    estimate_x = np.linspace(x.min(), x.max(), 100, endpoint=True)
    estimate_y = b0 + estimate_x * b1
    plt.title('y = {0:.4f} + {1:.4f} * x'.format(b0, b1))
    plt.plot(x, y, 'o')
    plt.plot(estimate_x, estimate_y, '.')
    plt.show()

def main():
    x = [81.8, 76.6, 76.6, 75.7, 73.8, 72.2, 71.2, 70.8, 68.5]
    y = [0.21, 0.58,  0.85, 0.68, 0.74, 0.93, 0.72, 1.22, 1.25]
    query_linear_regression(x, y)

if __name__ == "__main__":
    main()
```

## output
```
x: [81.8 76.6 76.6 75.7 73.8 72.2 71.2 70.8 68.5]
y: [0.21 0.58 0.85 0.68 0.74 0.93 0.72 1.22 1.25]
b0: 6.017831995165787
b1: -0.07041440041440661
y = 6.0178 + -0.0704 * x
x(80.0000) = 0.3847
```

![Figure 1](/assets/2019-10-22-statistics-for-business-and-economics-p14-06-Figure-1.png)

