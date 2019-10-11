---
layout: post
title: "pandas-dataframe-example"
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

## module version
```bash
bash-3.2$ pip3 list | grep pandas
pandas               0.25.1 
```

## layout of dataframe
### source
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
### output
```bash
    Name  Age
0    Tom   20
1   nick   21
2  krish   19
3   jack   18
```

## partial column
### source
```python
import pandas as pd

def main():
    data = {'Name':['Tom', 'nick', 'krish', 'jack'],
        'Age':[20, 21, 19, 18]}
    df = pd.DataFrame(data)
    print(df['Name'])

if __name__ == "__main__":
    main()
```

### output
```bash
0      Tom
1     nick
2    krish
3     jack
Name: Name, dtype: object
```

