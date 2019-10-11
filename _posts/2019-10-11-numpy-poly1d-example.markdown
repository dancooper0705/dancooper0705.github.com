---
layout: post
title: "numpy-poly1d-example"
date:  2019-10-11 11:00:00  +0800
categories: [dev]
tags: [python, numpy, poly1d]
---

## what is numpy
A ptyhon package supporting extra numeric data

## what is numpy.poly1d
A class representing a one dimensional polynomial

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

## polynomial initialization
```bash
bash-3.2$ python3
Python 3.7.3 (default, Mar 27 2019, 09:23:39)
[Clang 10.0.0 (clang-1000.11.45.5)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import numpy as np
>>> p = np.poly1d([3, 4, 5])
>>> print(p)
   2
3 x + 4 x + 5
```

## polynomial mutiplication
```bash
>>> print(p*p)
   4      3      2
9 x + 24 x + 46 x + 40 x + 25
```

## polynomial derivation
```bash
>>> print(p.deriv())
6 x + 4
```

## polynomial integration
```bash
>>> print(p.integ())
   3     2
1 x + 2 x + 5 x
```

## polynomial evaluation
```bash
>>> print(p(1))
12
>>> print(p(2))
25
>>> print(p(0))
5
>>> print(p(1))
12
>>> print(p(2))
25
>>> print(p(3))
44
>>> print(p([0,1,2,3]))
[ 5 12 25 44]
```
