---
layout: post
title: "solve-linear-regression-with-convex-programmin"
date:  2019-10-22 20:00:00  +0800
categories: [dev]
tags: [statistics]
---

## synosis
```
Given an array of x and y. Find the linear equation with minimum SSE(sum of
squares due to error). Let the linear equation to be y = b0 + b1 * x.
Supposedly, SSE(b0, b1) is a convex function. So linear regression of two
variables is a convex programming whose objective function is SSE(b0, b1) and
the solution space is the two dimensional space of (b1, b2). It could be solved
by many methods such as gradient descent and ternary search. Below shows how to
solve it with formula, gradient descent, and ternary search, respectively.
```

## source
```python
import math
import scipy.stats
import numpy as np
import matplotlib.pyplot as plt

def query_SSE(x, y, b0, b1):
    num = x.size
    return np.sum([(y[i] - (b0 + b1 * x[i])) ** 2 for i in range(num)])

def query_SSR(x, y, b0, b1):
    num = x.size
    return np.sum([((b0 + b1 * x[i]) - y.mean()) ** 2 for i in range(num)])

def query_linear_regression_with_ternary_search_b1(x, y, b0):
    cnt = 128
    left = - (10.0 ** 5)
    right = (10.0 ** 5)
    while cnt > 0:
        m1 = left + (right - left) / 3
        m2 = left + (right - left) / 3 * 2
        if query_SSE(x, y, b0, m1) <= query_SSE(x, y, b0, m2):
            right = m2
        else:
            left = m1
        cnt = cnt - 1
    return left

def query_linear_regression_with_ternary_search(x, y):
    x = np.array(x, dtype=np.float64)
    y = np.array(y, dtype=np.float64)
    cnt = 128
    left = - (10.0 ** 5)
    right = (10.0 ** 5)
    while cnt > 0:
        m1 = left + (right - left) / 3
        m2 = left + (right - left) / 3 * 2
        p1 = query_linear_regression_with_ternary_search_b1(x, y, m1)
        p2 = query_linear_regression_with_ternary_search_b1(x, y, m2)
        if query_SSE(x, y, m1, p1) <= query_SSE(x, y, m2, p2):
            right = m2
        else:
            left = m1
        cnt = cnt - 1
    b0 = left
    b1 = query_linear_regression_with_ternary_search_b1(x, y, b0)
    SSE = query_SSE(x, y, b0, b1)
    SSR = query_SSR(x, y, b0, b1)
    SST = SSE + SSR
    r2 = SSR / SST
    r = 0
    if b1 >= 0:
        r = math.sqrt(r2)
    else:
        r = -math.sqrt(r2)
    print('query_linear_regression_with_ternary_search')
    print('x: ' + str(x))
    print('y: ' + str(y))
    print('b0: ' + str(b0))
    print('b1: ' + str(b1))
    print('y = {0:.4f} + {1:.4f} * x'.format(b0, b1))
    print('SST = {0:.4f}'.format(SST))
    print('SSR = {0:.4f}'.format(SSR))
    print('SSE = {0:.4f}'.format(SSE))
    print('r2 = {0:.4f}'.format(r2))
    print('r = {0:.4f}'.format(r))

def query_linear_regression_with_gradient_descent(x, y):
    num = len(x)
    x = np.array(x, dtype=np.float64)
    y = np.array(y, dtype=np.float64)
    eps = (0.1) ** 3 
    delta = (10.0) ** 5
    rate = 0.99
    pos = [100, 2000]
    while delta >= eps:
        #print('pos: ' + str(pos))
        #print('SSE: ' + str(query_SSE(x, y, pos[0], pos[1])))
        next_pos = []
        next_pos.append([pos[0] - delta, pos[1]])
        next_pos.append([pos[0] + delta, pos[1]])
        next_pos.append([pos[0], pos[1] - delta])
        next_pos.append([pos[0], pos[1] + delta])
        #print('next_pos: ' + str(next_pos))
        min_val = query_SSE(x, y, pos[0], pos[1])
        for i in range(4):
            val = query_SSE(x, y, next_pos[i][0], next_pos[i][1])
            if val < min_val:
                min_val = val
                pos = next_pos[i]
        delta = delta * rate
    b0 = pos[0]
    b1 = pos[1]
    SSE = query_SSE(x, y, b0, b1)
    SSR = query_SSR(x, y, b0, b1)
    SST = SSE + SSR
    r2 = SSR / SST
    r = 0
    if b1 >= 0:
        r = math.sqrt(r2)
    else:
        r = -math.sqrt(r2)
    print('query_linear_regression_with_gradient_descent')
    print('x: ' + str(x))
    print('y: ' + str(y))
    print('b0: ' + str(b0))
    print('b1: ' + str(b1))
    print('y = {0:.4f} + {1:.4f} * x'.format(b0, b1))
    print('SST = {0:.4f}'.format(SST))
    print('SSR = {0:.4f}'.format(SSR))
    print('SSE = {0:.4f}'.format(SSE))
    print('r2 = {0:.4f}'.format(r2))
    print('r = {0:.4f}'.format(r))

def query_linear_regression_with_formula(x, y):
    num = len(x)
    x = np.array(x, dtype=np.float64)
    y = np.array(y, dtype=np.float64)
    xy = x * y
    xx = x * x
    yy = y * y
    print('query_linear_regression_with_formula')
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
    query_linear_regression_with_formula(x, y)
    print()
    query_linear_regression_with_ternary_search(x, y)
    print()
    query_linear_regression_with_gradient_descent(x, y)
    print()

if __name__ == "__main__":
    main()
```

## output
```
query_linear_regression_with_formula
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

query_linear_regression_with_ternary_search
x: [2.6 3.4 3.6 3.2 3.5 2.9]
y: [2800. 3100. 3500. 3000. 3400. 3100.]
b0: 1290.5405318436833
b1: 581.0810839343185
y = 1290.5405 + 581.0811 * x
SST = 335000.0025
SSR = 249864.8673
SSE = 85135.1351
r2 = 0.7459
r = 0.8636

query_linear_regression_with_gradient_descent
x: [2.6 3.4 3.6 3.2 3.5 2.9]
y: [2800. 3100. 3500. 3000. 3400. 3100.]
b0: -870.4333505994366
b1: 1250.2444971217692
y = -870.4334 + 1250.2445 * x
SST = 1577828.3830
SSR = 1159019.3252
SSE = 418809.0577
r2 = 0.7346
r = 0.8571
```
