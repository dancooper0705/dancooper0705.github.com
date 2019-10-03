---
layout: post
title: "python-imaging-library"
date:  2019-10-03 19:00:00  +0800
categories: [dev]
tags: [python, image]
---

## environment
macOS High Sierra
{% highlight bash %}
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.13.6
BuildVersion:   17G4015
{% endhighlight %}

## what is python imaging library
PIL(Python Imaging Library) is a python package which could help open and edit image files. The support file formats are png, gif and etc.

## how to install
{% highlight bash %}
bash-3.2$ pip3 install pillow
Requirement already satisfied: pillow in /usr/local/lib/python3.7/site-packages (6.2.0)
bash-3.2$ pip3 list | grep Pillow
Pillow               6.2.0
{% endhighlight %}

## sample program to open a image
{% highlight python %}
from PIL import Image

def main():
    img = Image.open('a.png')
    img.show()
    print(img.format)
    print(img.mode)
if __name__ == "__main__":
    main()

{% endhighlight %}

## sample program to blur a image
{% highlight python %}
from PIL import Image, ImageFilter

def main():
    img = Image.open('a.png')
    blurred = img.filter(ImageFilter.BLUR)
    blurred.show()

if __name__ == "__main__":
    main()
{% endhighlight %}


## sample program to rotate a image counter-clockwise 90 degrees
{% highlight python %}
from PIL import Image, ImageFilter

def main():
    img = Image.open('a.png')
    rotated90 = img.rotate(90)
    rotated90.show()

if __name__ == "__main__":
    main()
{% endhighlight %}
