---
layout: post
title: "python-init-different-collections"
date:  2019-10-02 11:00:00  +0800
categories: [dev]
tags: [python]
---

## synosis
sample code to initializae different collcections in python.

## environment
{% highlight bash %}
bash-3.2$ python3 --version
Python 3.7.3
{% endhighlight %}

## explanation
* (13, 'c', 'str') is a tuple.
* [1, 2, 3] is a list.
* {12, 13} is a set.
* {13: 15} is a dict.
* set() is an empty set.
* {} is an empty dict.

## source
{% highlight ruby %}
import sys 
import math
import re
import io

def main():
    a = (13, 'c', "str")
    print(a)
    print(type(a))
    b = [1, 2, 3]
    print(b)
    print(type(b))
    c = {13, 12} 
    print(c)
    print(type(c))
    d = {13: 12, 13: 15} 
    print(d)
    print(type(d))
    e = set()
    print(e)
    print(type(e))
    f = {}
    print(f)
    print(type(f))
if __name__ == "__main__":
    main()
{% endhighlight %}

## output
{% highlight ruby %}
bash-3.2$ python3 a.py
(13, 'c', 'str')
<class 'tuple'>
[1, 2, 3]
<class 'list'>
{12, 13}
<class 'set'>
{13: 15}
<class 'dict'>
set()
<class 'set'>
{}
<class 'dict'>
{% endhighlight %}
