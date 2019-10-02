---
layout: post
title: "open-image-files-in-command-line-in-macos"
date:  2019-10-02 10:10:00  +0800
tags: [dev]
tags: [bash]
---

## environment
macOS 10.13.6 High Sierra
{% highlight bash %}
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.13.6
BuildVersion:   17G4015
{% endhighlight %}

## open image with Preview
{% highlight bash %}
bash-3.2$ open a.jpg
{% endhighlight %}

## open image with Pixelmator
{% highlight bash %}
bash-3.2$ open -a Pixelmator a.jpg
{% endhighlight %}

## open image with Quick Look Server debug and management tool
{% highlight bash %}
bash-3.2$ qlmanage -p a.jpg 
Testing Quick Look preview with files:
        a.jpg
{% endhighlight %}
