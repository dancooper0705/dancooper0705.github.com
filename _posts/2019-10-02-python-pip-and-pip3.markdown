---
layout: post
title: "python-pip-and-pip3"
date:  2019-10-02 18:00:00  +0800
categories: [dev]
tags: [python]
---

## what is pip
python package manager

## what is pip3
python package manager for python3

## environment
{% highlight bash %}
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.13.6
BuildVersion:   17G4015
{% endhighlight %}

## pip and pip3
* By default, the Mac OS X High Siera 10.13.6 uses python 2.7. pip helps manage python2 modules.
* python3 and pip3 are installed also by default. pip3 help manage python3 modules.
{% highlight bash %}
bash-3.2$ pip --version
pip 19.2.3 from /Library/Python/2.7/site-packages/pip-19.2.3-py2.7.egg/pip (python 2.7)
bash-3.2$ pip3 --version
pip 19.0.3 from /usr/local/lib/python3.7/site-packages/pip (python 3.7)
{% endhighlight %}

