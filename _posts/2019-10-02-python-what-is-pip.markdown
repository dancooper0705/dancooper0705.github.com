---
layout: post
title: "python-what-is-pip"
date:  2019-10-02 12:00:00  +0800
categories: [dev]
tags: [python]
---

## what is pip
a python package manager

## environment
{% highlight bash %}
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.13.6
BuildVersion:   17G4015
{% endhighlight %}

## install pip with easy_install
{% highlight bash %}
bash-3.2$ sudo easy_install pip
Password:
Searching for pip
Reading https://pypi.python.org/simple/pip/
Best match: pip 19.2.3
Downloading https://files.pythonhosted.org/packages/00/9e/4c83a0950d8bdec0b4ca72afd2f9cea92d08eb7c1a768363f2ea458d08b4/pip-19.2.3.tar.gz#sha256=e7a31f147974362e6c82d84b91c7f2bdf57e4d3163d3d454e6c3e71944d67135
Processing pip-19.2.3.tar.gz
Writing /tmp/easy_install-byxCZO/pip-19.2.3/setup.cfg
Running pip-19.2.3/setup.py -q bdist_egg --dist-dir /tmp/easy_install-byxCZO/pip-19.2.3/egg-dist-tmp-pJKlYa
/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/distutils/dist.py:267: UserWarning: Unknown distribution option: 'python_requires'
  warnings.warn(msg)
  warning: no files found matching 'docs/docutils.conf'
  warning: no previously-included files found matching '.coveragerc'
  warning: no previously-included files found matching '.mailmap'
  warning: no previously-included files found matching '.appveyor.yml'
  warning: no previously-included files found matching '.travis.yml'
  warning: no previously-included files found matching 'tox.ini'
  warning: no files found matching 'Makefile' under directory 'docs'
  warning: no files found matching '*.bat' under directory 'docs'
  warning: no previously-included files found matching 'src/pip/_vendor/six'
  warning: no previously-included files found matching 'src/pip/_vendor/six/moves'
  warning: no previously-included files matching '*.pyi' found under directory 'src/pip/_vendor'
  no previously-included directories found matching '.github'
  no previously-included directories found matching '.azure-pipelines'
  no previously-included directories found matching 'docs/build'
  no previously-included directories found matching 'news'
  no previously-included directories found matching 'tasks'
  no previously-included directories found matching 'tests'
  no previously-included directories found matching 'tools'
  creating /Library/Python/2.7/site-packages/pip-19.2.3-py2.7.egg
  Extracting pip-19.2.3-py2.7.egg to /Library/Python/2.7/site-packages
  Adding pip 19.2.3 to easy-install.pth file
  Installing pip script to /usr/local/bin
  Installing pip2.7 script to /usr/local/bin
  Installing pip2 script to /usr/local/bin

  Installed /Library/Python/2.7/site-packages/pip-19.2.3-py2.7.egg
  Processing dependencies for pip
  Finished processing dependencies for pip
{% endhighlight %}


## install python packages
bash-3.2$ pip install package_name
{% highlight bash %}
bash-3.2$ pip install package_name
{% endhighlight %}

## uninstall python packages
{% highlight bash %}
bash-3.2$ pip uninstall package_name
{% endhighlight %}

## list installed python packages
{% highlight bash %}
bash-3.2$  pip list
DEPRECATION: Python 2.7 will reach the end of its life on January 1st, 2020. Please upgrade your Python as Python 2.7 won't be maintained after that date. A future version of pip will drop support for Python 2.7. More details about Python 2 support in pip, can be found at https://pip.pypa.io/en/latest/development/release-process/#python-2-support
Package                                Version 
-------------------------------------- --------
altgraph                               0.10.2  
bdist-mpkg                             0.5.0   
bonjour-py                             0.3     
macholib                               1.5.1   
matplotlib                             1.3.1   
modulegraph                            0.10.4  
numpy                                  1.8.0rc1
pip                                    19.2.3  
py2app                                 0.7.3   
pyobjc-core                            2.5.1   
pyobjc-framework-Accounts              2.5.1   
pyobjc-framework-AddressBook           2.5.1   
pyobjc-framework-AppleScriptKit        2.5.1   
pyobjc-framework-AppleScriptObjC       2.5.1   
pyobjc-framework-Automator             2.5.1   
pyobjc-framework-CFNetwork             2.5.1   
pyobjc-framework-Cocoa                 2.5.1   
pyobjc-framework-Collaboration         2.5.1   
pyobjc-framework-CoreData              2.5.1   
pyobjc-framework-CoreLocation          2.5.1   
pyobjc-framework-CoreText              2.5.1   
pyobjc-framework-DictionaryServices    2.5.1   
pyobjc-framework-EventKit              2.5.1   
pyobjc-framework-ExceptionHandling     2.5.1   
pyobjc-framework-FSEvents              2.5.1   
pyobjc-framework-InputMethodKit        2.5.1   
pyobjc-framework-InstallerPlugins      2.5.1   
pyobjc-framework-InstantMessage        2.5.1   
pyobjc-framework-LatentSemanticMapping 2.5.1   
pyobjc-framework-LaunchServices        2.5.1   
pyobjc-framework-Message               2.5.1   
pyobjc-framework-OpenDirectory         2.5.1   
pyobjc-framework-PreferencePanes       2.5.1   
pyobjc-framework-PubSub                2.5.1   
pyobjc-framework-QTKit                 2.5.1   
pyobjc-framework-Quartz                2.5.1   
pyobjc-framework-ScreenSaver           2.5.1   
pyobjc-framework-ScriptingBridge       2.5.1   
pyobjc-framework-SearchKit             2.5.1   
pyobjc-framework-ServiceManagement     2.5.1   
pyobjc-framework-Social                2.5.1   
pyobjc-framework-SyncServices          2.5.1   
pyobjc-framework-SystemConfiguration   2.5.1   
pyobjc-framework-WebKit                2.5.1   
pyOpenSSL                              0.13.1  
pyparsing                              2.0.1   
python-dateutil                        1.5     
pytz                                   2013.7  
scipy                                  0.13.0b1
setuptools                             18.5    
six                                    1.4.1   
xattr                                  0.6.4   
zope.interface                         4.1.1   
{% endhighlight %}
