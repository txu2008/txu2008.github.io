---
layout: post
title:  "md5sum递归生成整个目录的sum"
date:   2015-02-16 20:14:54
categories: Linux
tags: md5sum
---

* content
{:toc}

使用md5sum递归生成整个目录的sum


```
find ./ -type f -print0 | xargs -0 md5sum > ./my.md5
md5sum -c my.md5
md5sum -c my.md5| grep -v OK
```