---
layout: post
title:  "Linux 显示git当前分支"
date:   2015-02-15 22:14:54
categories: Linux
tags: git
---

* content
{:toc}

通过修改 ~/.bashrc 显示git当前分支


在~/.bashrc 末尾添加：
```
function git-branch-name {
	  git symbolic-ref HEAD 2>/dev/null | cut -d"/" -f 3
}
function git-branch-prompt {
	  local branch=`git-branch-name`
	  if [ $branch ]; then printf " (%s)" $branch; fi
}
PS1="\u@\h:\[\033[0;36m\]\w\[\033[0m\]\[\033[0;32m\]\$(git-branch-prompt)\[\033[0m\]# "
```
source ~/.bashrc

效果：
```
root@txuvm1:~/test (master)# cd bd_unit/
root@txuvm1:~/test/bd_unit (master)# 
```
