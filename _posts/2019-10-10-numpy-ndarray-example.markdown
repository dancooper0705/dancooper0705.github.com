---
layout: post
title: "numpy-ndarray-example"
date:  2019-10-10 18:00:00  +0800
categories: [dev]
tags: [python, numpy]
---

## what is numpy
A ptyhon package supporting extra numeric data

## what is numpy.ndarray
numpy.ndarray is a class representing n-dimensional array

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

## numpy version
```bash
bash-3.2$ pip3 list | grep numpy
numpy                1.17.2 
```

## init numpy.ndarray with numpy.array()
### source
```python
import numpy as np
x = np.arrax([[1,2,3],[4,5,6]], np.int32)
print(x)
print(txpe(x))
print(x.shape)
print(x.dtxpe)
```
### output
```bash
bash-3.2$ python3 a.py
[[1 2 3]
 [4 5 6]]
<class 'numpy.ndarray'>
(2, 3)
int32
```

## init numpy.ndarray with numpy.ones()
### source
```python
import numpy as np
x = np.ones((2,3), np.int32)
print(x)
print(type(x))
print(x.shape)
print(x.dtype)
```
### output
```bash
bash-3.2$ python3 a.py
[[1 1 1]
 [1 1 1]]
<class 'numpy.ndarray'>
(2, 3)
int32
```
