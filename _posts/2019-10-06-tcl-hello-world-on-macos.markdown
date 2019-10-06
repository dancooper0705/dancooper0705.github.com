---
layout: post
title: "tcl-hello-world-on-macos"
date:  2019-10-06 17:00:00  +0800
categories: [dev]
tags: [tcl]
---

## environment
macOS High Sierra
{% highlight bash %}
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.13.6
BuildVersion:   17G4015
{% endhighlight %}

## tclsh version
{% highlight bash %}
bash-3.2$ tclsh 
%  puts $tcl_version
8.5
{% endhighlight %}

## what is tcl
a general purpose interpreted script languge.

## what is tclsh
a shell which interpretes tcl script

## source
{% highlight tcl %}
#!/usr/bin/tclsh
puts "Hello World!"
{% endhighlight %}

## output
{% highlight bash %}
bash-3.2$ tclsh a.tcl
Hello World!
{% endhighlight %}
