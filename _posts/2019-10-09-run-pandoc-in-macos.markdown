---
layout: post
title: "run-pandoc-in-macos"
date:  2019-10-09 14:00:00  +0800
categories: [dev]
tags: [pandoc]
---

## what is pandoc
A universal document converter

## environment
macOS High Sierra
```bash
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.13.6
BuildVersion:   17G4015
```

## install pandoc in macOS
```bash
bash-3.2$ brew install pandoc
Updating Homebrew...
==> Downloading https://homebrew.bintray.com/bottles/pandoc-2.7.3.high_sierra.bottle.tar.gz
==> Downloading from https://akamai.bintray.com/af/afe8cc21378449f87f55d10a36282018038e8ad9240b2c10cae28586760ea2e1?__gda__=exp=1570603968~hmac=e6fb3d53f844b357b9218e1a448f068aa3a4f5d90f6679be1b9e8a52cf3d2902&response-content-disposition=
######################################################################## 100.0%
==> Pouring pandoc-2.7.3.high_sierra.bottle.tar.gz
==> Caveats
Bash completion has been installed to:
/usr/local/etc/bash_completion.d
==> Summary
�  /usr/local/Cellar/pandoc/2.7.3: 179 files, 75.5MB
==> `brew cleanup` has not been run in 30 days, running now...
Removing: /Users/chengyihe/Library/Caches/Homebrew/gcc@7--7.4.0.high_sierra.bottle.tar.gz... (75.4MB)
Removing: /Users/chengyihe/Library/Caches/Homebrew/gdbm--1.18.1.high_sierra.bottle.1.tar.gz... (192.3KB)
Removing: /Users/chengyihe/Library/Caches/Homebrew/libmpc--1.1.0.high_sierra.bottle.tar.gz... (114.2KB)
Removing: /Users/chengyihe/Library/Caches/Homebrew/openssl--1.0.2r.high_sierra.bottle.tar.gz... (3.7MB)
Removing: /Users/chengyihe/Library/Caches/Homebrew/openssl--1.0.2s.high_sierra.bottle.tar.gz... (3.7MB)
Removing: /Users/chengyihe/Library/Caches/Homebrew/openssl@1.1--1.1.1c.high_sierra.bottle.tar.gz... (5.2MB)
Removing: /Users/chengyihe/Library/Caches/Homebrew/pkg-config--0.29.2.high_sierra.bottle.tar.gz... (235.8KB)
Removing: /Users/chengyihe/Library/Caches/Homebrew/python--3.7.3.high_sierra.bottle.tar.gz... (14.6MB)
Removing: /Users/chengyihe/Library/Caches/Homebrew/readline--8.0.0_1.high_sierra.bottle.tar.gz... (516.9KB)
Removing: /Users/chengyihe/Library/Caches/Homebrew/ruby--2.6.3.high_sierra.bottle.tar.gz... (9.2MB)
Removing: /Users/chengyihe/Library/Caches/Homebrew/ruby-build--20190828.tar.gz... (61.5KB)
Removing: /Users/chengyihe/Library/Caches/Homebrew/sqlite--3.28.0.high_sierra.bottle.tar.gz... (1.8MB)
Removing: /Users/chengyihe/Library/Caches/Homebrew/xz--5.2.4.high_sierra.bottle.tar.gz... (372.7KB)
Removing: /Users/chengyihe/Library/Logs/Homebrew/pkg-config... (64B)
Removing: /Users/chengyihe/Library/Logs/Homebrew/gdbm... (64B)
Removing: /Users/chengyihe/Library/Logs/Homebrew/python... (3 files, 132.6KB)
Removing: /Users/chengyihe/Library/Logs/Homebrew/libyaml... (64B)
Removing: /Users/chengyihe/Library/Logs/Homebrew/readline... (64B)
Removing: /Users/chengyihe/Library/Logs/Homebrew/ruby-build... (2 files, 179B)
Removing: /Users/chengyihe/Library/Logs/Homebrew/xz... (64B)
Removing: /Users/chengyihe/Library/Logs/Homebrew/autoconf... (64B)
Removing: /Users/chengyihe/Library/Logs/Homebrew/openssl@1.1... (64B)
Removing: /Users/chengyihe/Library/Logs/Homebrew/openssl... (64B)
Removing: /Users/chengyihe/Library/Logs/Homebrew/ruby... (64B)
Removing: /Users/chengyihe/Library/Logs/Homebrew/rbenv... (64B)
Pruned 0 symbolic links and 18 directories from /usr/local
```

## check pandoc version
```bash
bash-3.2$ pandoc --version
pandoc 2.7.3
Compiled with pandoc-types 1.17.5.4, texmath 0.11.2.2, skylighting 0.8.1
Default user data directory: /Users/chengyihe/.local/share/pandoc or /Users/chengyihe/.pandoc
Copyright (C) 2006-2019 John MacFarlane
Web:  http://pandoc.org
This is free software; see the source for copying conditions.
There is no warranty, not even for merchantability or fitness
for a particular purpose.
```

## pandoc usage
```bash
pandoc [OPTIONS] [FILES]
  -f FORMAT, -r FORMAT  --from=FORMAT, --read=FORMAT                    
  -t FORMAT, -w FORMAT  --to=FORMAT, --write=FORMAT                     
  -o FILE               --output=FILE                                   
                        --wrap=auto|none|preserve                       
  -s                    --standalone                                    
                        --template=FILE                                 
                        --data-dir=DIRECTORY                            
  -M KEY[:VALUE]        --metadata=KEY[:VALUE]                          
                        --metadata-file=FILE                            
  -V KEY[:VALUE]        --variable=KEY[:VALUE]                          
                        --ascii                                         
                        --toc, --table-of-contents                      
                        --toc-depth=NUMBER                              
  -N                    --number-sections                               
                        --number-offset=NUMBERS                         
                        --top-level-division=section|chapter|part       
                        --extract-media=PATH                            
                        --resource-path=SEARCHPATH                      
  -H FILE               --include-in-header=FILE                        
  -B FILE               --include-before-body=FILE                      
  -A FILE               --include-after-body=FILE                       
                        --no-highlight                                  
                        --highlight-style=STYLE|FILE                    
                        --syntax-definition=FILE                        
                        --dpi=NUMBER                                    
                        --eol=crlf|lf|native                            
                        --columns=NUMBER                                
  -p                    --preserve-tabs                                 
                        --tab-stop=NUMBER                               
                        --pdf-engine=PROGRAM                            
                        --pdf-engine-opt=STRING                         
                        --reference-doc=FILE                            
                        --self-contained                                
                        --request-header=NAME:VALUE                     
                        --file-scope                                    
                        --abbreviations=FILE                            
                        --indented-code-classes=STRING                  
                        --default-image-extension=extension             
  -F PROGRAM            --filter=PROGRAM                                
                        --lua-filter=SCRIPTPATH                         
                        --base-header-level=NUMBER                      
                        --strip-empty-paragraphs                        
                        --track-changes=accept|reject|all               
                        --strip-comments                                
                        --reference-links                               
                        --reference-location=block|section|document     
                        --atx-headers                                   
                        --listings                                      
  -i                    --incremental                                   
                        --slide-level=NUMBER                            
                        --section-divs                                  
                        --html-q-tags                                   
                        --email-obfuscation=none|javascript|references  
                        --id-prefix=STRING                              
  -T STRING             --title-prefix=STRING                           
  -c URL                --css=URL
                        --epub-subdirectory=DIRNAME
                        --epub-cover-image=FILE
                        --epub-metadata=FILE
                        --epub-embed-font=FILE
                        --epub-chapter-level=NUMBER
                        --ipynb-output=all|none|best
                        --bibliography=FILE
                        --csl=FILE                                      
                        --citation-abbreviations=FILE                   
                        --natbib                                        
                        --biblatex                                      
                        --mathml                                        
                        --webtex[=URL]                                  
                        --mathjax[=URL]                                 
                        --katex[=URL]                                   
                        --gladtex                                       
                        --trace                                         
                        --dump-args                                     
                        --ignore-args                                   
                        --verbose                                       
                        --quiet                                         
                        --fail-if-warnings                              
                        --log=FILE                                      
                        --bash-completion                               
                        --list-input-formats                            
                        --list-output-formats                           
                        --list-extensions[=FORMAT]                      
                        --list-highlight-languages                      
                        --list-highlight-styles                         
  -D FORMAT             --print-default-template=FORMAT                 
                        --print-default-data-file=FILE                  
                        --print-highlight-style=STYLE|FILE              
  -v                    --version                                       
  -h                    --help       
```
