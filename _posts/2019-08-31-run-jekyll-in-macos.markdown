---
layout: post
title: "run-jekyll-in-macos"
date:  2019-08-31 11:12:00  +0800
categories: [dev]
tags: [jekyll]
---

## objective
Run Jekyll in macOS.

## environment
macOS 10.13.6 High Sierra
{% highlight bash %}
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.13.6
BuildVersion:   17G4015
{% endhighlight %}

## install jekyll
[install jekyll in macOS](install-jekyll-in-macos.html)

## use jekyll to create new blog
{% highlight bash %}
bash-3.2$ jekyll new myblog
Running bundle install in /Users/dancooper/Workspace/test/myblog...
  Bundler: Fetching gem metadata from https://rubygems.org/...........
  Bundler: Fetching gem metadata from https://rubygems.org/.
  Bundler: Resolving dependencies...
  Bundler: Using public_suffix 4.0.1
  Bundler: Using addressable 2.7.0
  Bundler: Using bundler 1.17.2
  Bundler: Using colorator 1.1.0
  Bundler: Using concurrent-ruby 1.1.5
  Bundler: Using eventmachine 1.2.7
  Bundler: Using http_parser.rb 0.6.0
  Bundler: Using em-websocket 0.5.1
  Bundler: Using ffi 1.11.1
  Bundler: Using forwardable-extended 2.6.0
  Bundler: Using i18n 1.6.0
  Bundler: Using sassc 2.2.0
  Bundler: Using jekyll-sass-converter 2.0.0
  Bundler: Using rb-fsevent 0.10.3
  Bundler: Using rb-inotify 0.10.0
  Bundler: Using ruby_dep 1.5.0
  Bundler: Using listen 3.1.5
  Bundler: Using jekyll-watch 2.2.1
  Bundler: Using kramdown 2.1.0
  Bundler: Using kramdown-parser-gfm 1.1.0
  Bundler: Using liquid 4.0.3
  Bundler: Using mercenary 0.3.6
  Bundler: Using pathutil 0.16.2
  Bundler: Using rouge 3.9.0
  Bundler: Using safe_yaml 1.0.5
  Bundler: Using unicode-display_width 1.6.0
  Bundler: Using terminal-table 1.8.0
  Bundler: Using jekyll 4.0.0
  Bundler: Using jekyll-feed 0.12.1
  Bundler: Using jekyll-seo-tag 2.6.1
  Bundler: Using minima 2.5.1
  Bundler: Bundle complete! 6 Gemfile dependencies, 31 gems now installed.
  Bundler: Use `bundle info [gemname]` to see where a bundled gem is installed.
New jekyll site installed in /Users/dancooper/Workspace/test/myblog.
{% endhighlight %}

## run jekyll
{% highlight bash %}
bash-3.2$ cd myblog/
bash-3.2$ jekyll serve
Configuration file: /Users/dancooper/Workspace/test/myblog/_config.yml
            Source: /Users/dancooper/Workspace/test/myblog
       Destination: /Users/dancooper/Workspace/test/myblog/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
       Jekyll Feed: Generating feed for posts
                    done in 0.291 seconds.
 Auto-regeneration: enabled for '/Users/dancooper/Workspace/test/myblog'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
{% endhighlight %}

