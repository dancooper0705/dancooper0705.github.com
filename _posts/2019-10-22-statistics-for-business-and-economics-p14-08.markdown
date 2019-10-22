---
layout: post
title: "statistics-for-business-and-economics-p14-08"
date:  2019-10-22 18:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
Nielsen Media Research collects data showing which advertiser get the most
exopsoure during prime-time TV on ABC, CBS, NBC, Fox, UPN, and WB networks. Data
showing the number of household exporures in millions and the number of times
the ad was aired for the week of April 28-May 4, 1997, follow (USA Today, May 5,
1997).
```

Advertiesed Brand | Times Ad Aired | Household Exposures
--- | --- | ---
Wendy's | 28 | 191.7
Ford Escort | 20 | 174.6
Austin Powers movie | 14 | 161.3
Nissan | 16 | 161.1
Pizza Hut | 16 | 147.7
Saturn | 16 | 146.3
Father's Day movie | 11 | 138.2

```
a. Develop the estimated regression equation showing how the number of times an
ad is aired is related to the number of household exposures.
b. Provide an interpretation for the slope of the estimated regression equation.
c. What is the estimated number of household exposures if an ad is aired 15
times?
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
    print('x({0:.4f}) = {1:.4f}'.format(15.0, b0 + b1 * 15.0))
    estimate_x = np.linspace(x.min(), x.max(), 100, endpoint=True)
    estimate_y = b0 + estimate_x * b1
    plt.title('y = {0:.4f} + {1:.4f} * x'.format(b0, b1))
    plt.plot(x, y, 'o')
    plt.plot(estimate_x, estimate_y, '.')
    plt.show()

def main():
    x = [28, 20, 14, 16, 16, 16, 11]
    y = [191.7, 174.6, 161.3, 161.1, 147.7, 146.3, 138.2]
    query_linear_regression(x, y)

if __name__ == "__main__":
    main()
```

## output
```
x: [28. 20. 14. 16. 16. 16. 11.]
y: [191.7 174.6 161.3 161.1 147.7 146.3 138.2]
b0: 107.12600644122392
b1: 3.066264090177128
y = 107.1260 + 3.0663 * x
x(15.0000) = 153.1200
```

![Figure 1](/assets/2019-10-22-statistics-for-business-and-economics-p14-08-Figure-1.png)

