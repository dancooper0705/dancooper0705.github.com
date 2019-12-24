---
layout: post
title: "python-datetime-timedelta"
date:  2019-12-24 15:00:00  +0800
categories: [dev]
tags: [python, datetime]
---

## question
**Day difference of two date**
```
Given two dates, return the day difference.
```

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
bash-3.2$ python3
Python 3.7.4 (default, Sep  7 2019, 18:29:04) 
[Clang 10.0.0 (clang-1000.11.45.5)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

## example
```python
>>> import datetime
>>> date1 = datetime.date(1912, 1, 1)
>>> date2 = datetime.date(2019,12,24)
>>> delta = date2 - date1
>>> print(type(delta))
<class 'datetime.timedelta'>
>>> print(delta)
39439 days, 0:00:00
>>> print(delta.days)
39439
```
