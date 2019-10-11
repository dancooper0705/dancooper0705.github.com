---
layout: post
title: "install-scipy-in-macos"
date:  2019-10-11 10:00:00  +0800
categories: [dev]
tags: [python, scipy]
---

## what is scipy
A pyton package which implement a scitific ecosystem.

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

## install scipy
```bash
bash-3.2$ pip3 search scipy
scipy (1.3.1)                - SciPy: Scientific Library for Python
bash-3.2$ pip3 install scipy
Collecting scipy
  Downloading https://files.pythonhosted.org/packages/d5/06/1a696649f4b2e706c509cb9333fdc6331fbe71251cede945f9e1fa13ea34/scipy-1.3.1-cp37-cp37m-macosx_10_6_intel.macosx_10_9_intel.macosx_10_9_x86_64.macosx_10_10_intel.macosx_10_10_x86_64.whl (27.7MB)
      100% |████████████████████████████████| 27.7MB 1.8MB/s 
      Requirement already satisfied: numpy>=1.13.3 in /usr/local/lib/python3.7/site-packages (from scipy) (1.17.2)
      Installing collected packages: scipy
      Successfully installed scipy-1.3.1
```
