---
layout: post
title: "vi-edit-file-in-binary-mode"
date:  2019-10-02 15:00:00  +0800
categories: [dev]
tags: [vi]
---

## synopsis
This post shows how to edit files in binary mode.

## environment
{% highlight bash %}
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.13.6
BuildVersion:   17G4015
{% endhighlight %}

## create a binary file
{% highlight bash %}
bash-3.2$ dd if=/dev/zero of=a.out bs=16 count=2
2+0 records in
2+0 records out
32 bytes transferred in 0.000069 secs (462820 bytes/sec)
{% endhighlight %}

## use vi to open file with binary mode
{% highlight bash %}
bash-3.2$ vi -b a.out
^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@
{% endhighlight %}

## feed buffer contents into the standard input of xxd and replace the original buffer with the standard output of xxd
{% highlight vi %}
:%!xxd
00000000: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000010: 0000 0000 0000 0000 0000 0000 0000 0000  ................
{% endhighlight %}

## update the second byte as 0xab
{% highlight vi %}
00000000: 00ab 0000 0000 0000 0000 0000 0000 0000  ................
00000010: 0000 0000 0000 0000 0000 0000 0000 0000  ................
{% endhighlight %}


## feed buffer contents into the standard input of xxd -r and replace the original buffer with the standard output of xxd -r
{% highlight vi %}
:%!xxd -r
^@<ab>^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@
{% endhighlight %}

## save and close the file
{% highlight vi %}
:wq
{% endhighlight %}

## xxd shows the binary file is updated as expected
{% highlight vi %}
bash-3.2$ xxd a.out
00000000: 00ab 0000 0000 0000 0000 0000 0000 0000  ................
00000010: 0000 0000 0000 0000 0000 0000 0000 0000  ................
{% endhighlight %}
