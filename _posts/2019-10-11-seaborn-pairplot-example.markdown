---
layout: post
title: "seaborn-pairplot-example"
date:  2019-10-11 20:00:00  +0800
categories: [dev]
tags: [python, seaborn]
---

## what is seaborn
A ptyhon package which visualize data analysis. It's based on matplotlib package.

## what is seaborn-pairplot
A function to draw correlation of two variables

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

## install seaborn
```bash
bash-3.2$ pip3 install seaborn
Collecting seaborn
  Downloading https://files.pythonhosted.org/packages/a8/76/220ba4420459d9c4c9c9587c6ce607bf56c25b3d3d2de62056efe482dadc/seaborn-0.9.0-py3-none-any.whl (208kB)
    100% |████████████████████████████████| 215kB 841kB/s
Requirement already satisfied: matplotlib>=1.4.3 in /usr/local/lib/python3.7/site-packages (from seaborn) (3.1.1)
Requirement already satisfied: scipy>=0.14.0 in /usr/local/lib/python3.7/site-packages (from seaborn) (1.3.1)
Requirement already satisfied: numpy>=1.9.3 in /usr/local/lib/python3.7/site-packages (from seaborn) (1.17.2)
Requirement already satisfied: pandas>=0.15.2 in /usr/local/lib/python3.7/site-packages (from seaborn) (0.25.1)
Requirement already satisfied: pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=2.0.1 in /usr/local/lib/python3.7/site-packages (from matplotlib>=1.4.3->seaborn) (2.4.2)
Requirement already satisfied: cycler>=0.10 in /usr/local/lib/python3.7/site-packages (from matplotlib>=1.4.3->seaborn) (0.10.0)
Requirement already satisfied: kiwisolver>=1.0.1 in /usr/local/lib/python3.7/site-packages (from matplotlib>=1.4.3->seaborn) (1.1.0)
Requirement already satisfied: python-dateutil>=2.1 in /usr/local/lib/python3.7/site-packages (from matplotlib>=1.4.3->seaborn) (2.8.0)
Requirement already satisfied: pytz>=2017.2 in /usr/local/lib/python3.7/site-packages (from pandas>=0.15.2->seaborn) (2019.2)
Requirement already satisfied: six in /usr/local/lib/python3.7/site-packages (from cycler>=0.10->matplotlib>=1.4.3->seaborn) (1.12.0)
Requirement already satisfied: setuptools in /usr/local/lib/python3.7/site-packages (from kiwisolver>=1.0.1->matplotlib>=1.4.3->seaborn) (41.2.0)
Installing collected packages: seaborn
Successfully installed seaborn-0.9.0
```
## module version
```bash
bash-3.2$ pip3 list | grep -E "(seaborn|panda)"
pandas               0.25.1
seaborn              0.9.0
```
