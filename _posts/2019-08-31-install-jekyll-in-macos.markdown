---
layout: post
title: "install-jekyll-in-macos"
date:  2019-08-31 11:12:00  +0800
categories: ruby
---

## objective
Install Jekyll in macOS.

## environment
macOS 10.13.6 High Sierra
{% highlight bash %}
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.13.6
BuildVersion:   17G4015
{% endhighlight %}

## install ruby if its version is not >= 2.0.0
Make sure that ruby version is >= 2.4.0. By default, the ruby version in macOS High Sierra is only 2.3.x. See below posts to install newer version of ruby environment.
* [install-ruby-with-homebrew-in-macos](install-ruby-with-homebrew-in-macos.html)
* [install-ruby-with-rbenv-in-macos](install-ruby-with-rbenv-in-macos.html)

## set path environment
{% highlight bash %}
bash-3.2$ export PATH=/usr/local/opt/ruby/bin:$PATH
bash-3.2$ ruby -v
ruby 2.6.3p62 (2019-04-16 revision 67580) [x86_64-darwin17]
bash-3.2$ export PATH=$HOME/.gem/ruby/2.6.0/bin:$PATH
bash-3.2$ echo $PATH
/Users/dancooper/.gem/ruby/2.6.0/bin:/usr/local/opt/ruby/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
{% endhighlight %}

## check if RubyGems’s path environment variable contains ~/.gem/ruby/2.6.0/bin
{% highlight bash %}
bash-3.2$ gem env
RubyGems Environment:
  - RUBYGEMS VERSION: 3.0.3
  - RUBY VERSION: 2.6.3 (2019-04-16 patchlevel 62) [x86_64-darwin17]
  - INSTALLATION DIRECTORY: /usr/local/lib/ruby/gems/2.6.0
  - USER INSTALLATION DIRECTORY: /Users/dancooper/.gem/ruby/2.6.0
  - RUBY EXECUTABLE: /usr/local/opt/ruby/bin/ruby
  - GIT EXECUTABLE: /usr/bin/git
  - EXECUTABLE DIRECTORY: /usr/local/lib/ruby/gems/2.6.0/bin
  - SPEC CACHE DIRECTORY: /Users/dancooper/.gem/specs
  - SYSTEM CONFIGURATION DIRECTORY: /usr/local/Cellar/ruby/2.6.3/etc
  - RUBYGEMS PLATFORMS:
    - ruby
    - x86_64-darwin-17
  - GEM PATHS:
     - /usr/local/lib/ruby/gems/2.6.0
     - /Users/dancooper/.gem/ruby/2.6.0
     - /usr/local/Cellar/ruby/2.6.3/lib/ruby/gems/2.6.0
  - GEM CONFIGURATION:
     - :update_sources => true
     - :verbose => true
     - :backtrace => false
     - :bulk_threshold => 1000
  - REMOTE SOURCES:
     - https://rubygems.org/
  - SHELL PATH:
     - /Users/dancooper/.gem/ruby/2.6.0/bin
     - /usr/local/opt/ruby/bin
     - /usr/local/bin
     - /usr/bin
     - /bin
     - /usr/sbin
     - /sbin
{% endhighlight %}

## install jeykll
{% highlight bash %}
bash-3.2$ gem install --user-install bundler jekyll
Successfully installed bundler-2.0.2
Parsing documentation for bundler-2.0.2
Done installing documentation for bundler after 1 seconds
Fetching jekyll-sass-converter-2.0.0.gem
Fetching sassc-2.2.0.gem
Fetching ffi-1.11.1.gem
Fetching jekyll-watch-2.2.1.gem
Fetching ruby_dep-1.5.0.gem
Fetching rb-inotify-0.10.0.gem
Fetching rb-fsevent-0.10.3.gem
Fetching listen-3.1.5.gem
Fetching kramdown-2.1.0.gem
Fetching kramdown-parser-gfm-1.1.0.gem
Fetching liquid-4.0.3.gem
Fetching mercenary-0.3.6.gem
Fetching forwardable-extended-2.6.0.gem
Fetching pathutil-0.16.2.gem
Fetching rouge-3.9.0.gem
Fetching safe_yaml-1.0.5.gem
Fetching jekyll-4.0.0.gem
Fetching unicode-display_width-1.6.0.gem
Fetching terminal-table-1.8.0.gem
Successfully installed public_suffix-3.1.1
Successfully installed addressable-2.6.0
Successfully installed colorator-1.1.0
Building native extensions. This could take a while...
Successfully installed http_parser.rb-0.6.0
Building native extensions. This could take a while...
Successfully installed eventmachine-1.2.7
Successfully installed em-websocket-0.5.1
Successfully installed concurrent-ruby-1.1.5
 
HEADS UP! i18n 1.1 changed fallbacks to exclude default locale.
But that may break your application.
 
Please check your Rails app for 'config.i18n.fallbacks = true'.
If you're using I18n (>= 1.1.0) and Rails (< 5.2.2), this should be
'config.i18n.fallbacks = [I18n.default_locale]'.
If not, fallbacks will be broken in your app by I18n 1.1.x.
 
For more info see:
https://github.com/svenfuchs/i18n/releases/tag/v1.1.0
 
Successfully installed i18n-1.6.0
Building native extensions. This could take a while...
Successfully installed ffi-1.11.1
Building native extensions. This could take a while...
Successfully installed sassc-2.2.0
Successfully installed jekyll-sass-converter-2.0.0
Successfully installed ruby_dep-1.5.0
Successfully installed rb-inotify-0.10.0
Successfully installed rb-fsevent-0.10.3
Successfully installed listen-3.1.5
Successfully installed jekyll-watch-2.2.1
Successfully installed kramdown-2.1.0
Successfully installed kramdown-parser-gfm-1.1.0
Successfully installed liquid-4.0.3
Successfully installed mercenary-0.3.6
Successfully installed forwardable-extended-2.6.0
Successfully installed pathutil-0.16.2
Successfully installed rouge-3.9.0
Successfully installed safe_yaml-1.0.5
Successfully installed unicode-display_width-1.6.0
Successfully installed terminal-table-1.8.0
Successfully installed jekyll-4.0.0
Parsing documentation for public_suffix-3.1.1
Installing ri documentation for public_suffix-3.1.1
Parsing documentation for addressable-2.6.0
Installing ri documentation for addressable-2.6.0
Parsing documentation for colorator-1.1.0
Installing ri documentation for colorator-1.1.0
Parsing documentation for http_parser.rb-0.6.0
unknown encoding name "chunked\r\n\r\n25" for ext/ruby_http_parser/vendor/http-parser-java/tools/parse_tests.rb, skipping
Installing ri documentation for http_parser.rb-0.6.0
Parsing documentation for eventmachine-1.2.7
Installing ri documentation for eventmachine-1.2.7
Parsing documentation for em-websocket-0.5.1
Installing ri documentation for em-websocket-0.5.1
Parsing documentation for concurrent-ruby-1.1.5
Installing ri documentation for concurrent-ruby-1.1.5
Parsing documentation for i18n-1.6.0
Installing ri documentation for i18n-1.6.0
Parsing documentation for ffi-1.11.1
Installing ri documentation for ffi-1.11.1
Parsing documentation for sassc-2.2.0
Installing ri documentation for sassc-2.2.0
Parsing documentation for jekyll-sass-converter-2.0.0
Installing ri documentation for jekyll-sass-converter-2.0.0
Parsing documentation for ruby_dep-1.5.0
Installing ri documentation for ruby_dep-1.5.0
Parsing documentation for rb-inotify-0.10.0
Installing ri documentation for rb-inotify-0.10.0
Parsing documentation for rb-fsevent-0.10.3
Installing ri documentation for rb-fsevent-0.10.3
Parsing documentation for listen-3.1.5
Installing ri documentation for listen-3.1.5
Parsing documentation for jekyll-watch-2.2.1
Installing ri documentation for jekyll-watch-2.2.1
Parsing documentation for kramdown-2.1.0
Installing ri documentation for kramdown-2.1.0
Parsing documentation for kramdown-parser-gfm-1.1.0
Installing ri documentation for kramdown-parser-gfm-1.1.0
Parsing documentation for liquid-4.0.3
Installing ri documentation for liquid-4.0.3
Parsing documentation for mercenary-0.3.6
Installing ri documentation for mercenary-0.3.6
Parsing documentation for forwardable-extended-2.6.0
Installing ri documentation for forwardable-extended-2.6.0
Parsing documentation for pathutil-0.16.2
Installing ri documentation for pathutil-0.16.2
Parsing documentation for rouge-3.9.0
Installing ri documentation for rouge-3.9.0
Parsing documentation for safe_yaml-1.0.5
Installing ri documentation for safe_yaml-1.0.5
Parsing documentation for unicode-display_width-1.6.0
Installing ri documentation for unicode-display_width-1.6.0
Parsing documentation for terminal-table-1.8.0
Installing ri documentation for terminal-table-1.8.0
Parsing documentation for jekyll-4.0.0
Installing ri documentation for jekyll-4.0.0
Done installing documentation for public_suffix, addressable, colorator, http_parse
{% endhighlight %}
