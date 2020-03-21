---
layout: post
title: "Linux Command"
subtitle: ''
comments: false
author: "Gump"
header-style: text
date: 2020-3-20 20:30:21 +0800
tags:
    - Linux
    - 笔记
---

# Linux-Command

## man

查看所有命令的使用方法

## grep

-A num, --after-context=num
             Print num lines of trailing context after each match.  See also the -B and -C options.

-B num, --before-context=num
             Print num lines of leading context before each match.  See also the -A and -C options.

-C[num, --context=num]
             Print num lines of leading and trailing context surrounding each match.  The default is 2 and is equivalent to -A 2 -B 2.  Note: no whitespace maybe given between the option and its argument.

## awk

是一门解释型的编程语言

它依次处理文件的每一行，并读取里面的每一个字段

$0 代表一整行；$1、$2、...$n 代表通过空格或者制表符分割后的字段

-F 指定分割符

NF 代表当前行有多少个字段 $NF代表最后一个字段值

NR 表示当前处理的第几行

tolower()、toupper()、length()....

## WC

统计命令

-c The number of bytes

-l The number of lines

-m The number of characters

-w The number of words

## uniq

过滤掉重复

