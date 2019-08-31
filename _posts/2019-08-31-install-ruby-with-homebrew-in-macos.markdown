---
layout: post
title:  "install-ruby-with-homebrew-in-macos"
date:   2019-08-31 09:40:00  +0800
categories: [dev]
tags: [ruby]
---

## objective
Install different version of ruby with homebrew in macOS.

## motivation
The default ruby version in macOS High Sierra is 2.3.x, but some ruby packages requires ruby >= 2.4.0

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
search t
{% endhighlight %}

## search for the latest ruby with homebrew
Search for the latest ruby formulae.
{% highlight bash %}
bash-3.2$ brew search ruby
==> Formulae
chruby                                          jruby                                           rbenv-bundler-ruby-version                      ruby-completion                                 ruby@2.4
chruby-fish                                     mruby                                           ruby                                            ruby-install                                    ruby@2.5
imessage-ruby                                   mruby-cli                                       ruby-build                                      ruby@2.0                                        homebrew/portable-ruby/portable-ruby
{% endhighlight %}

## install ruby with homebrew
{% highlight bash %}
bash-3.2$ brew install ruby
Updating Homebrew...
==> Auto-updated Homebrew!
Updated 1 tap (homebrew/core).
No changes to formulae.
 
==> Installing dependencies for ruby: libyaml and openssl
==> Installing ruby dependency: libyaml
==> Downloading https://homebrew.bintray.com/bottles/libyaml-0.2.2.high_sierra.bottle.tar.gz
######################################################################## 100.0%
==> Pouring libyaml-0.2.2.high_sierra.bottle.tar.gz
�  /usr/local/Cellar/libyaml/0.2.2: 9 files, 299.3KB
==> Installing ruby dependency: openssl
==> Downloading https://homebrew.bintray.com/bottles/openssl-1.0.2s.high_sierra.bottle.tar.gz
==> Downloading from https://akamai.bintray.com/b7/b72b8d9e582713d909936d7236542b366f07d800f8ec0eaa2d487a95c4e93bd9?__gda__=exp=1567160628~hmac=36684a9499ce29638d606c9e1656dd658a012d1c7a55729490d34bf99c67d5c8&response-content-disposition=
######################################################################## 100.0%
==> Pouring openssl-1.0.2s.high_sierra.bottle.tar.gz
==> Caveats
A CA file has been bootstrapped using certificates from the SystemRoots
keychain. To add additional certificates (e.g. the certificates added in
the System keychain), place .pem files in
  /usr/local/etc/openssl/certs
 
and run
  /usr/local/opt/openssl/bin/c_rehash
 
openssl is keg-only, which means it was not symlinked into /usr/local,
because Apple has deprecated use of OpenSSL in favor of its own TLS and crypto libraries.
 
If you need to have openssl first in your PATH run:
  echo 'export PATH="/usr/local/opt/openssl/bin:$PATH"' >> ~/.bash_profile
 
For compilers to find openssl you may need to set:
  export LDFLAGS="-L/usr/local/opt/openssl/lib"
  export CPPFLAGS="-I/usr/local/opt/openssl/include"
 
==> Summary
�  /usr/local/Cellar/openssl/1.0.2s: 1,795 files, 12.1MB
==> Installing ruby
==> Downloading https://homebrew.bintray.com/bottles/ruby-2.6.3.high_sierra.bottle.tar.gz
==> Downloading from https://akamai.bintray.com/52/52face1cf238072f1964cb6ace624510008857c645dee162ad0b60a138b6c136?__gda__=exp=1567160639~hmac=498e0b0c5fcb78be1e94fb54af58e82a2de9cc301c08881beb7fdb2f7be6e3dc&response-content-disposition=
######################################################################## 100.0%^[[A
==> Pouring ruby-2.6.3.high_sierra.bottle.tar.gz
==> Caveats
By default, binaries installed by gem will be placed into:
  /usr/local/lib/ruby/gems/2.6.0/bin
 
You may want to add this to your PATH.
 
ruby is keg-only, which means it was not symlinked into /usr/local,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.
 
If you need to have ruby first in your PATH run:
  echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bash_profile
 
For compilers to find ruby you may need to set:
  export LDFLAGS="-L/usr/local/opt/ruby/lib"
  export CPPFLAGS="-I/usr/local/opt/ruby/include"
 
==> Summary
�  /usr/local/Cellar/ruby/2.6.3: 19,372 files, 32.4MB
==> Caveats
==> openssl
A CA file has been bootstrapped using certificates from the SystemRoots
keychain. To add additional certificates (e.g. the certificates added in
the System keychain), place .pem files in
  /usr/local/etc/openssl/certs
 
and run
  /usr/local/opt/openssl/bin/c_rehash
 
openssl is keg-only, which means it was not symlinked into /usr/local,
because Apple has deprecated use of OpenSSL in favor of its own TLS and crypto libraries.
 
If you need to have openssl first in your PATH run:
  echo 'export PATH="/usr/local/opt/openssl/bin:$PATH"' >> ~/.bash_profile
 
For compilers to find openssl you may need to set:
  export LDFLAGS="-L/usr/local/opt/openssl/lib"
  export CPPFLAGS="-I/usr/local/opt/openssl/include"
 
==> ruby
By default, binaries installed by gem will be placed into:
  /usr/local/lib/ruby/gems/2.6.0/bin
 
You may want to add this to your PATH.
 
ruby is keg-only, which means it was not symlinked into /usr/local,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.
 
If you need to have ruby first in your PATH run:
  echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bash_profile
 
For compilers to find ruby you may need to set:
  export LDFLAGS="-L/usr/local/opt/ruby/lib"
  export CPPFLAGS="-I/usr/local/opt/ruby/include"
{% endhighlight %}

## add local ruby path to path environment variable
{% highlight bash %}
bash-3.2$ export PATH=/usr/local/opt/ruby/bin:$PATH
{% endhighlight %}

## check ruby version after homebrew installation 
It shows that the ruby 2.6 is installed in local developing directory. After we add the local binary ruby path before the path variable, we could use the ruby 2.6 in /usr/local/opt/ruby/bin/ruby instead of ruby 2.3 in /usr/bin/ruby.
{% highlight bash %}
bash-3.2$ which ruby
/usr/local/opt/ruby/bin/ruby
bash-3.2$ ruby -v
ruby 2.6.3p62 (2019-04-16 revision 67580) [x86_64-darwin17]
{% endhighlight %}

## the ruby version is still 2.3.x in new shell 
So far our current shell shows that the ruby version is 2.6.x. But if we open a new terminal whose shell reloads the $PATH environment variable, then it shows that the ruby version is still 2.3.x. Don’t worry, this situation is what we want, otherwise, it might affect other ruby projects which works well in ruby 2.3.x.
