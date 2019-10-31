---
layout: post
title: "java-regular-expression-example"
date:  2019-10-31 21:00:00  +0800
categories: [dev]
tags: [java, regular expression]
---

## environment
macOS Mojave
```bash
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.14.2
BuildVersion:   18C54
```

## python version
```bash
bash-3.2$ javac --version
javac 11.0.1
bash-3.2$ java --version
java 11.0.1 2018-10-16 LTS
Java(TM) SE Runtime Environment 18.9 (build 11.0.1+13-LTS)
Java HotSpot(TM) 64-Bit Server VM 18.9 (build 11.0.1+13-LTS, mixed mode)
```

## string matching and show all capturing groups
Each group is enclosed by a pair of Parentheses.
### source
```java
import java.io.*;
import java.util.*;
import java.math.*;
import java.lang.*;
import java.util.regex.*;
import java.awt.geom.*;

class Main
{
    public static void main (String args[]) {
        Scanner sc = new Scanner(System.in);
        String pattern = "(\\d+)\\.(\\d+)";
        String str = sc.next();
        Pattern r = Pattern.compile(pattern);
        Matcher m = r.matcher(str);
        System.out.println(str);
        System.out.println(pattern);
        while (m.find()) {
            System.out.println(m.group());
            for (int i = 1; i <= m.groupCount(); i++)
                System.out.println(i + ":[" + m.group(i) + "]");
        }
    }

}
```
### output
```bash
bash-3.2$ cat a.txt
a1111.5b234.001c567.32
bash-3.2$ java Main
^C^Cbash-3.2$ 
bash-3.2$ cat a.txt 
a1111.5b234.001c567.32
bash-3.2$ cat a.txt | java Main
a1111.5b234.001c567.32
(\d+)\.(\d+)
1111.5
1:[1111]
2:[5]
234.001
1:[234]
2:[001]
567.32
1:[567]
2:[32]
```

## string matching and replace all matched with replacement
### source
```
import java.io.*;
import java.util.*;
import java.math.*;
import java.lang.*;
import java.util.regex.*;
import java.awt.geom.*;

class Main
{
    public static void main (String args[]) {
        Scanner sc = new Scanner(System.in);
        String pattern = "(\\d+)\\.(\\d+)";
        String str = sc.next();
        Pattern r = Pattern.compile(pattern);
        Matcher m = r.matcher(str);
        System.out.println(str);
        System.out.println(pattern);
        System.out.println(m.replaceAll("(RealNumber)"));
    }

}
```
### output
```bash
bash-3.2$ cat a.txt 
a1111.5b234.001c567.32
bash-3.2$ cat a.txt | java Main
a1111.5b234.001c567.32
(\d+)\.(\d+)
a(RealNumber)b(RealNumber)c(RealNumber)
```
