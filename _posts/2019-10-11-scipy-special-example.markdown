---
layout: post
title: "scipy-special-example"
date:  2019-10-11 12:00:00  +0800
categories: [dev]
tags: [python, scipy]
---

## what is scipy
A python package named Scientific Library for Python

## what is scipy.special
A sub-package of scipy which has almost all mathematical functions

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

## scipy version
```bash
bash-3.2$ pip3 list | grep scipy
scipy                1.3.1  
```

## combination(n, k)
```bash
bash-3.2$ python3
Python 3.7.3 (default, Mar 27 2019, 09:23:39)
[Clang 10.0.0 (clang-1000.11.45.5)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import scipy
>>> import scipy.special
>>> scipy.special.comb(5,2)
10.0
```

## permutation(n, k)
```bash
>>> scipy.special.perm(5,2)
20.0
```

## factorial
```bash
>>> scipy.special.factorial(6)
array(720.)
```
