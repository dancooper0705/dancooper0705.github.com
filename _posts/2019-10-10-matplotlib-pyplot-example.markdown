---
layout: post
title: "matplotlib-pyplot-example"
date:  2019-10-10 19:00:00  +0800
categories: [dev]
tags: [python, matplotlib]
---

## what is matplotlib
A python package for 2D plotting

## what is matplotlib.pyplot
A python module providing matlab-like plotting functions

## environment
macOS High Sierra
```bash
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.13.6
BuildVersion:   17G4015
```

## python version
```bash
bash-3.2$ python3 --version
Python 3.7.3
```

## matplotlib version
```bash
bash-3.2$ pip3 list | grep matplotlib
matplotlib           3.1.1
```

## source
```python
import numpy as np
import matplotlib.pyplot as plt
N = 100
x = np.linspace(-10, 10, N, endpoint=True)
y = x * x
plt.title('y=x^2')
plt.plot(x, y, 'o')
plt.show()
```

## output
![alt text](/assets/2019-10-10-matplotlib-pyplot-example-figure-1.png)
