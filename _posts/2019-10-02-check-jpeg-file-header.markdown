---
layout: post
title: "check-jpeg-file-header"
date:  2019-10-02 15:35:00  +0800
categories: [dev]
tags: [image]
---

## synopsis
This post shows how to check jpeg header.

## environment
{% highlight bash %}
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.13.6
BuildVersion:   17G4015
{% endhighlight %}

## prepare a jpeg file
{% highlight bash %}
bash-3.2$ file a.jpg
a.jpg: JPEG image data, JFIF standard 1.01, aspect ratio, density 1x1, segment length 16, baseline, precision 8, 1080x1920, frames 3
{% endhighlight %}

## use xxd to see the file in hex base format
* The first two bytes of jpeg files ff d8 means SOI(Start Of Image).
* The 7th to 10th bytes shows JFIF. This image is jpeg jfif file.
* The last two bytes of jpeg files ff d9 means EOI (End Of Image).
{% highlight bash %}
bash-3.2$ xxd a.jpg | less
00000000: ffd8 ffe0 0010 4a46 4946 0001 0100 0001  ......JFIF......
00000010: 0001 0000 ffdb 0043 0001 0101 0101 0101  .......C........
00000020: 0101 0101 0101 0101 0101 0101 0101 0101  ................
00000030: 0101 0101 0101 0101 0101 0101 0101 0101  ................
00000040: 0101 0101 0101 0101 0101 0101 0101 0101  ................
00000050: 0101 0101 0101 0101 01ff db00 4301 0101  ............C...
......
001034c0: 72f8 7a35 276c 826c 9200 6169 9482 c407  r.z5'l.l..ai....
001034d0: 2287 76cf 416e 712a 7453 0015 4f50 2403  ".v.Anq*tS..OP$.
001034e0: 6496 b816 70b6 2d87 8fff d9              d...p.-....
{% endhighlight %}
