---
layout: post
title: "pandas-dataframe-example"
date:  2019-10-11 20:30:00  +0800
categories: [dev]
tags: [python, panda]
---

## what is pandas
A python package which has data struceture for data analysis

## what is pandas.dataframe
A class representing two-dimensional data structure. In addition to two-dimeional data, it also store rwo  and column information.

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

## construct dataframe from dict
```
>>> d = {'col1': [1, 2, 3], 'col2': [4, 5, 6], 'col3': [7, 8, 9]}
>>> df = pd.DataFrame(data=d)
>>> df
   col1  col2  col3
0     1     4     7
1     2     5     8
2     3     6     9
```

## construct dataframe from list
```
>>> df = pd.DataFrame(data=[[1,2,3],[4,5,6],[7,8,9]], index=['row1','row2','roe2'], columns=['col1','col2','col3'])
>>> df
      col1  col2  col3
row1     1     2     3
row2     4     5     6
roe2     7     8     9
```

## retrive columns of the dataframe
```
>>> df[['col1', 'col2']]
      col1  col2
row1     1     2
row2     4     5
roe2     7     8
```

## retrive rows of the dataframe
```
>>> df.loc[['row1', 'row2']]
      col1  col2  col3
row1     1     2     3
row2     4     5     6
```

## retrive information related to row, columan and data type
```
>>> df.index
Index(['row1', 'row2', 'roe2'], dtype='object')
>>> df.columns
Index(['col1', 'col2', 'col3'], dtype='object')
>>> df.dtypes
col1    int64
col2    int64
col3    int64
dtype: object
```
