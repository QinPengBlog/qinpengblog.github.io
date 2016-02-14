---
layout: post
title: 增加网站的推荐模块
date: 2016-02-14 18:23
categories: blog
tags: [个人主页]
description: 记录增加的过程。

---

参考[《Setting up this blog site: github, jekyll, and the hpstr theme》](http://nicolaroberts.github.io/website-setup-post/)和[《利用github-pages建立个人博客》](http://coolshell.info/blog/2015/03/github-pages-blog.html)，将Google analytics 和Google verify在"_config.yml"中设置如下：

    <# Analytics and webmaster tools stuff goes here
    google_analytics: UA-73781127-1
    google_verify: <meta name="google-site-verification" content="f-xallGRfKu4KN9VgwJYGRZprRAHyGPUIIz6O4A9Yck" />
    # https://ssl.bing.com/webmaster/configure/verify/ownership Option 2 content= goes here
    bing_verify: <meta name="msvalidate.01" content="731D1E6005EE00E5770F4B5909254F51" />
    />

参考[《为 Jekyll 添加百度统计》](http://havee.me/internet/2013-07/add-baidu-analytics-for-jekyll.html)编写"_config.yml"：

    <# Analytics and webmaster tools stuff goes here
    analytics :
      provider : Baidu
    google_analytics: UA-73781127-1
    google_verify: <meta name="google-site-verification" content="f-xallGRfKu4KN9VgwJYGRZprRAHyGPUIIz6O4A9Yck" />
    # https://ssl.bing.com/webmaster/configure/verify/ownership Option 2 content= goes here
    bing_verify: <meta name="msvalidate.01" content="731D1E6005EE00E5770F4B5909254F51" />
    />

Done.
---










