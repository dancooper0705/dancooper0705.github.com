---
layout: post
title:  "ssh-keygen"
date:   2019-08-30 08:47:38  +0800
categories: openssh
---

## What is open-ssh?
A suite of command line tools for ssh protocol.

## What is ssh-keygen?
ssh-keygen is a command line tool within open-ssh. It creates a pair of assymmetric keys for secure communications with ssh protocol.

## How it works?
By default, it creates a public key as ~/.ssh/id_rsa.pub and a private key as ~/.ssh/id_rsa.

{% highlight ruby %}
bash-3.2$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/username/.ssh/id_rsa):
{% endhighlight %}
