---
layout: post
title: "run-graphviz-in-macos"
date:  2019-10-12 20:00:00  +0800
categories: [dev]
tags: [graphviz]
---

## what is graphviz
A package to draw graph

## environment
macOS High Sierra
```bash
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.13.6
BuildVersion:   17G4015
```

## install graphviz in macOS
```bash
bash-3.2$ brew install graphviz
```

## commadn line tools of graphviz
```
bash-3.2$ man dot
DOT(1)                                                                                                                                                                                                          DOT(1)

NAME
       dot - filter for drawing directed graphs
       neato - filter for drawing undirected graphs
       twopi - filter for radial layouts of graphs
       circo - filter for circular layout of graphs
       fdp - filter for drawing undirected graphs
       sfdp - filter for drawing large undirected graphs
       patchwork - filter for squarified tree maps
       osage - filter for array-based layouts

SYNOPSIS
       dot [options] [files]
       neato [options] [files]
       twopi [options] [files]
       circo [options] [files]
       fdp [options] [files]
       sfdp [options] [files]
       patchwork [options] [files]
       osage [options] [files]

DESCRIPTION
       These  are  a collection of programs for drawing graphs.  There is actually only one main program; the specific layout algorithms are implemented as plugins. Thus, they largely share all of the same command-
       line options.
```
