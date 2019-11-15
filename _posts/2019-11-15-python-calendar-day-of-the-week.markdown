---
layout: post
title: "python-calendar-day-of-the-week.markdown"
date:  2019-11-15 17:00:00  +0800
categories: [dev]
tags: [python, calendar]
---

## question
```
[Day of the week]
Given a date, return the corresponding day of the week for that date.
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

## source & output
```python
>>> import calendar
>>> calendar.day_name[calendar.weekday(2019, 11, 15)]
'Friday'
```
