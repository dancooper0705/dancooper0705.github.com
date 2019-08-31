---
layout: post
title: "install-ruby-with-rbenv-in-macos"
date:  2019-08-31 10:55:00  +0800
categories: ruby
---

## objective
Install different version of ruby with rbenv in macOS.

## motivation
The default ruby version in High Sierra is 2.3.x, but the ruby package we need requires ruby >= 2.4.0

## environment 
macOS 10.13.6 High Sierra
{% highlight bash %}
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.13.6
BuildVersion:   17G4015
{% endhighlight %}

## check system ruby version 
The default version of ruby in macOS 10.13, i.e., High Sierra, is 2.3.x.
{% highlight bash %}
bash-3.2$ which ruby
/usr/bin/ruby
bash-3.2$ ruby -v
ruby 2.3.7p456 (2018-03-28 revision 63024) [universal.x86_64-darwin17]
{% endhighlight %}

## install rbenv with homebrew
{% highlight bash %}
bash-3.2$ brew install rbenv
==> Installing dependencies for rbenv: autoconf, openssl@1.1, pkg-config and ruby-build
==> Installing rbenv dependency: autoconf
==> Downloading https://homebrew.bintray.com/bottles/autoconf-2.69.high_sierra.bottle.4.tar.gz
==> Downloading from https://akamai.bintray.com/63/63957a3952b7af5496012b3819c9956822fd7d895d63339c23fdc65c502e1a40?__gda__=exp=1567162631~hmac=95339463b3a00c6d09a92ffe0141831992648f51deee69647de505d654aa99ca&response-content-disposition=
######################################################################## 100.0%
==> Pouring autoconf-2.69.high_sierra.bottle.4.tar.gz
==> Caveats
Emacs Lisp files have been installed to:
  /usr/local/share/emacs/site-lisp/autoconf
  ==> Summary
  �  /usr/local/Cellar/openssl@1.1/1.1.1c: 7,963 files, 17.9MB
  ==> Installing rbenv dependency: pkg-config
  ==> Downloading https://homebrew.bintray.com/bottles/pkg-config-0.29.2.high_sierra.bottle.tar.gz
  ==> Downloading from https://akamai.bintray.com/f1/f1b29fb5388dccab0fcaf665ab43d308ee51816b24262417bf83a686b6e308ae?__gda__=exp=1567162680~hmac=1e2b0956c538856d0276fa548b40c49810fc0143ece65dd8b3bf3fa1e612e696&response-content-disposition=
######################################################################## 100.0%
  ==> Pouring pkg-config-0.29.2.high_sierra.bottle.tar.gz
  �  /usr/local/Cellar/pkg-config/0.29.2: 11 files, 627.2KB
  ==> Installing rbenv dependency: ruby-build
  ^[[A^[[A^[[A^[[A^[[B^[[B^[[B==> Downloading https://github.com/rbenv/ruby-build/archive/v20190828.tar.gz
  ==> Downloading from https://codeload.github.com/rbenv/ruby-build/tar.gz/v20190828
######################################################################## 100.0%
  ==> ./install.sh
  �  /usr/local/Cellar/ruby-build/20190828: 454 files, 227.4KB, built in 19 seconds
  ==> Installing rbenv
  ==> Downloading https://homebrew.bintray.com/bottles/rbenv-1.1.2.high_sierra.bottle.tar.gz
######################################################################## 100.0%
  ==> Pouring rbenv-1.1.2.high_sierra.bottle.tar.gz
  �  /usr/local/Cellar/rbenv/1.1.2: 36 files, 65KB
  ==> Caveats
  ==> autoconf
  Emacs Lisp files have been installed to:
    /usr/local/share/emacs/site-lisp/autoconf
    ==> openssl@1.1
    A CA file has been bootstrapped using certificates from the system
    keychain. To add additional certificates, place .pem files in
      /usr/local/etc/openssl@1.1/certs

  and run /usr/local/opt/openssl@1.1/bin/c_rehash

  openssl@1.1 is keg-only, which means it was not symlinked into
  /usr/local, because openssl/libressl is provided by macOS so don't
  link an incompatible version.

  If you need to have openssl@1.1 first in your PATH run: echo 'export
  PATH="/usr/local/opt/openssl@1.1/bin:$PATH"' >> ~/.bash_profile

  For compilers to find openssl@1.1 you may need to set: export
  LDFLAGS="-L/usr/local/opt/openssl@1.1/lib" export
  CPPFLAGS="-I/usr/local/opt/openssl@1.1/include"

  For pkg-config to find openssl@1.1 you may need to set:
  export
  PKG_CONFIG_PATH="/usr/local/opt/openssl@1.1/lib/pkgconfig"
{% endhighlight %}


## setup rbenv
{% highlight bash %}
bash-3.2$ rbenv init
# Load rbenv automatically by appending
# the following to ~/.bash_profile:
 
 eval "$(rbenv init -)"
{% endhighlight %}

## check rbenv installation
{% highlight bash %}
bash-3.2$ curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-doctor | bash
Checking for `rbenv' in PATH: /usr/local/bin/rbenv
Checking for rbenv shims in PATH: not found
  The directory `/Users/dancooper/.rbenv/shims' must be present in PATH for rbenv to work.
    Please run `rbenv init' and follow the instructions.
     
Checking `rbenv install' support: /usr/local/bin/rbenv-install (ruby-build 20190828)
Counting installed Ruby versions: none
    There aren't any Ruby versions installed under `/Users/dancooper/.rbenv/versions'.
    You can install Ruby versions like so: rbenv install 2.2.4
Checking RubyGems settings: OK
Auditing installed plugins: OK
{% endhighlight %}

## install ruby 2.6.3 with rbenv
{% highlight bash %}
bash-3.2$ rbenv install 2.6.3
ruby-build: using openssl from homebrew
Downloading ruby-2.6.3.tar.bz2...
-> https://cache.ruby-lang.org/pub/ruby/2.6/ruby-2.6.3.tar.bz2
Installing ruby-2.6.3...
ruby-build: using readline from homebrew
Installed ruby-2.6.3 to /Users/dancooper/.rbenv/versions/2.6.3
{% endhighlight %}

## use rbenv to select ruby version 2.6.3
{% highlight bash %}
bash-3.2$ rbenv global 2.6.3
bash-3.2$ rbenv global 
2.6.3
{% endhighlight %}
