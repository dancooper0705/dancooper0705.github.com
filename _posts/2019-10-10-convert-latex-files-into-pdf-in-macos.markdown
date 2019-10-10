---
layout: post
title: "run-latex-in-macos"
date:  2019-10-10 11:00:00  +0800
categories: [dev]
tags: [latex]
---

## what is latex
A document compiler.

## environment
macOS High Sierra
```bash
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.13.6
BuildVersion:   17G4015
```

## install latex in macOS
The latex distribution in macOS is MacTeX. The mactex-20190508.pkg could be downloaded from http://www.tug.org/mactex/. Just simply double click the pkg file in finder application and walk through the installation process.
```bash
bash-3.2$ latex --version
pdfTeX 3.14159265-2.6-1.40.20 (TeX Live 2019)
kpathsea version 6.3.1
Copyright 2019 Han The Thanh (pdfTeX) et al.
There is NO warranty.  Redistribution of this software is
covered by the terms of both the pdfTeX copyright and
the Lesser GNU General Public License.
For more information about these matters, see the file
named COPYING and the pdfTeX source.
Primary author of pdfTeX: Han The Thanh (pdfTeX) et al.
Compiled with libpng 1.6.36; using libpng 1.6.36
Compiled with zlib 1.2.11; using zlib 1.2.11
Compiled with xpdf version 4.01
```

## latex command line tools
After installing mactex, some command line tools are also installed.
```bash
bash-3.2$ man xelatex
LATEX(1)                                                                                                                                                                                                      LATEX(1)

NAME
       latex, pdflatex, xelatex, lualatex, dvilualatex, cslatex, pdfcslatex, platex, uplatex, lamed - structured text formatting and typesetting
```

## create a tex file
```bash
bash-3.2$ cat a.tex
\documentclass{article}

\begin{document}
First document. This is a simple example, with no
extra parameters or packages included.
\end{document}
```

## compile a tex file into a dvi file
```bash
bash-3.2$ latex a.tex
This is pdfTeX, Version 3.14159265-2.6-1.40.20 (TeX Live 2019) (preloaded format=latex)
 restricted \write18 enabled.
entering extended mode
(./a.tex
LaTeX2e <2018-12-01>
(/usr/local/texlive/2019/texmf-dist/tex/latex/base/article.cls
Document Class: article 2018/09/03 v1.4i Standard LaTeX document class
(/usr/local/texlive/2019/texmf-dist/tex/latex/base/size10.clo)) (./a.aux)
[1] (./a.aux) )
Output written on a.dvi (1 page, 340 bytes).
Transcript written on a.log.
```
## open dvi file
By default, open chooses TexShop to open dvi files
```bash
bash-3.2$ open a.dvi
```

## covert a dvi file into a pdf file
```bash
bash-3.2$ dvipdf a.dvi
bash-3.2$ ls a.pdf
a.pdf
```

## convert a dvi file into a postscript file
```bash
bash-3.2$ dvips a.dvi
This is dvips(k) 5.999 Copyright 2019 Radical Eye Software (www.radicaleye.com)
' TeX output 2019.10.10:1204' -> a.ps
</usr/local/texlive/2019/texmf-dist/dvips/base/tex.pro>
</usr/local/texlive/2019/texmf-dist/dvips/base/texps.pro>. 
</usr/local/texlive/2019/texmf-dist/fonts/type1/public/amsfonts/cm/cmr10.pfb>
[1] 
bash-3.2$ ls a.ps
a.ps
```

## use ghostscript to convert a postscript file into a pdf file
```bash
bash-3.2$ gs -sDEVICE=pdfwrite -sOutputFile=a.pdf a.ps
GPL Ghostscript 9.27 (2019-04-04)
Copyright (C) 2018 Artifex Software, Inc.  All rights reserved.
This software is supplied under the GNU AGPLv3 and comes with NO WARRANTY:
see the file COPYING for details.
>>showpage, press <return> to continue<<

GS>quit
bash-3.2$ ls a.pdf
a.pdf
```

## use utility script ps2pdf to convert a postscript file into a pdf file
```bash
bash-3.2$ ps2pdf a.ps
bash-3.2$ ls a.pdf
a.pdf
```
