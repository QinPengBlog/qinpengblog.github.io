---
layout: post
title: 解决Markdown标题的显示问题
date: 2016-02-16
categories: blog
tags: [个人网站, Markdown]
description: 记录了发现Markdown标题的显示问题及解决的过程。

---

本来以为Post的文章是可以正常读取Mardkdown的，然而打开查看的时候，发现post的文章也没有编译##，反而出现了代码高亮。

我要查看"_config.yml"的修改了。

查看完"_config.yml"，没有对主要地方进行更改。

重新查看了各个网页，发现只是部分格式不能读取Markdown，-可以正常显示为·，但是##不能编译为表示标题的格式。

重新看了一遍语法，发现似乎是我没有在##后面加上空格···

Done!

但是现在的问题是每个#标记的标题前都有#，即使只有一个#标记。

2016-02-17 14:39 

发现Tags.md等编译出来的页面里面没有#标记。问题应该出在"post.html"中。

---