---
layout: post
title: "panda-dataframe-example"
date:  2019-10-11 20:30:00  +0800
categories: [dev]
tags: [python, panda]
---

## what is panda
A python package which has data struceture for data analysis

## what is panda.dataframe
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
bash-3.2$ python3 --version
Python 3.7.3
```

## numpy version
```bash
bash-3.2$ pip3 list | grep numpy
numpy                1.17.2 
```

## source
```python
import pandas as pd

def main():
    data = {'Name':['Tom', 'nick', 'krish', 'jack'],
        'Age':[20, 21, 19, 18]}
    df = pd.DataFrame(data)
    print(df)

if __name__ == "__main__":
    main()
```

## output
```bash
    Name  Age
0    Tom   20
1   nick   21
2  krish   19
3   jack   18
```
