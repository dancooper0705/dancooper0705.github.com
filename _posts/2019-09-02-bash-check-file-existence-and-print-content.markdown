---
layout: post
title: "bash-check-file-existence-and-print-content"
date:  2019-09-02 17:20:00  +0800
categories: [dev]
tags: [bash]
---

## synosis
Some bash commands to check file existence and print its content

## environment
{% highlight bash %}
bash-3.2$ bash --version
GNU bash, version 3.2.57(1)-release (x86_64-apple-darwin17)
Copyright (C) 2007 Free Software Foundation, Inc.
{% endhighlight %}

## check if a file exist
The test command with -e parameter checks the existence of a file. If the file exists, the test command returns 0. Otherwise, it returns 1.
{% highlight bash %}
bash-3.2$ ls
a.bash          file.txt
bash-3.2$ test -e file.txt
bash-3.2$ echo $?
0
bash-3.2$ test -e test.txt
bash-3.2$ echo $?
1
{% endhighlight %}

## scripts to print file content
This script prints the file content line by line. It also prints the corresponding line number before each line.
{% highlight bash %}
#!/bin/bash

cnt=1

while read  LINE;
do
    echo ${cnt}: ${LINE}
    ((cnt++))
done < file.txt
{% endhighlight %}

## output
{% highlight bash %}
bash-3.2$ bash a.bash
1: Line 1
2: Line 2
3: Line 3
4: Line 4
5: Line 5
6: Line 6
7: Line 7
8: Line 8
9: Line 9
10: Line 10
{% endhighlight %}
