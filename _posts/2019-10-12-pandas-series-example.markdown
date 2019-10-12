---
layout: post
title: "pandas-series-example"
date:  2019-10-12 11:00:00  +0800
categories: [dev]
tags: [python, pandas]
---

## what is pandas
A python package which has data struceture for data analysis

## what is panda.series
A class representing one-dimensional data structure. In addition to data, it also store rwo  and column information. Each columnn of a pandas.Dataframe is a pandas.Series.

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
bash-3.2$ python3
Python 3.7.3 (default, Mar 27 2019, 09:23:39) 
[Clang 10.0.0 (clang-1000.11.45.5)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

## module version
```python
>>> import pandas as pd
>>> print(pd.__version__)
0.25.1
```

## construct Series from list
```
>>> series = pd.Series([1,2,3,4,5])
>>> series
0    1
1    2
2    3
3    4
4    5
dtype: int64
```

## basic operation of Series
```
>>> series = pd.Series([1,2,3,4,5])
>>> series.mean()
3.0
>>> series.unique()
array([1, 2, 3, 4, 5])
>>> series.dot([1,3,5,7,9])
95
```

## construct Series from DataFrame
```
>>> d = {'col1': [1, 2, 3], 'col2': [4, 5, 6], 'col3': [7, 8, 9]}
>>> df = pd.DataFrame(data=d)
>>> series = df['col2']
>>> series
0    4
1    5
2    6
Name: col2, dtype: int64
>>> series.mean()
5.0
>>> series.unique()
array([4, 5, 6])
>>> series.dot([1,2,3])
32
```
