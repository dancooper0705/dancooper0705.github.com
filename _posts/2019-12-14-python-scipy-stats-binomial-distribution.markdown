---
layout: post
title: "python-scipy-stats-binomial-distribution"
date:  2019-12-24 15:40:00  +0800
categories: [dev]
tags: [python, scipy]
---

## what is scipy.stats.binom
* scipy: a package supporting scientific computation
* stats: a module supporting statistics functions
* binom: a class supporting binomial distribution

## environment
macOS Mojave
```bash
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.14.2
BuildVersion:   18C54
```

## python version
```bash
bash-3.2$ python3 --version
Python 3.7.4
```

## package version
```bash
bash-3.2$ pip3 list | grep scipy
scipy                1.3.1
```

## source
```python
import math
import numpy as np
import scipy.stats

def main():
    n = 10
    p = 0.8
    print('binomial distribution: Probability mass function')
    for i in range(0, n + 1):
        print('n: %d, p: %f, pmf: %f' % (n, p, scipy.stats.binom.pmf(i, n, p).item()))

if __name__ == "__main__":
```

## output
```bash
bash-3.2$ python3 a.py
binomial distribution: Probability mass function
n: 10, p: 0.800000, pmf: 0.000000
n: 10, p: 0.800000, pmf: 0.000004
n: 10, p: 0.800000, pmf: 0.000074
n: 10, p: 0.800000, pmf: 0.000786
n: 10, p: 0.800000, pmf: 0.005505
n: 10, p: 0.800000, pmf: 0.026424
n: 10, p: 0.800000, pmf: 0.088080
n: 10, p: 0.800000, pmf: 0.201327
n: 10, p: 0.800000, pmf: 0.301990
n: 10, p: 0.800000, pmf: 0.268435
n: 10, p: 0.800000, pmf: 0.107374
```
