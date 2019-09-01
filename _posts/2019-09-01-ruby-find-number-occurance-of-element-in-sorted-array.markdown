---
layout: post
title: "ruby-find-number-occurance-of-element-in-sorted-array"
date:  2019-09-01 17:44:00  +0800
categories: [dev]
tags: [ruby]
---

## synosis
Find the number of occurance of an element in a sorted array.

## environment
ruby 2.6
{% highlight bash %}
bash-3.2$ ruby -v
ruby 2.6.3p62 (2019-04-16 revision 67580) [x86_64-darwin17]
{% endhighlight %}

## explanation
The first bineary search is to find the lower bound of satisfied indexes. The second binary search is to find the upper bound of satisfed indexes. The difference of the two bounds are the number of occurance of the element in this array. The time comlexity of this method is O(log n).

## source
{% highlight ruby %}
#! /usr/bin/ruby -w

arr = [1, 1, 1, 4, 4, 4, 9, 9, 9, 16, 16, 16, 25, 25, 25, 36, 36, 36, 49, 49, 49, 64, 64, 64, 81, 81, 81, 100, 100, 100]
a = 25
arr.sort!

puts "#{arr}"-

first = (0...arr.size).bsearch { |x| arr[x] >= a }
last = (0..arr.size).bsearch { |x| arr[x] > a }
total = last - first

puts "there are #{total} elements whose value is #{a}"
{% endhighlight %}

## output
{% highlight ruby %}
bash-3.2$ ruby a.rb
[1, 1, 1, 4, 4, 4, 9, 9, 9, 16, 16, 16, 25, 25, 25, 36, 36, 36, 49, 49, 49, 64, 64, 64, 81, 81, 81, 100, 100, 100]
there are 3 elements whose value is 25
{% endhighlight %}
