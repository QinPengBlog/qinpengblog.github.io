---
layout: post
title: 修改网站的评论模块
date: 2016-02-14
categories: blog
tags: [个人主页]
description: 记录修改的过程。

---

看了[《使用Github Pages建独立博客》](http://beiyuu.com/github-pages/)文章，它里面使用的是Disqus的评论模块，并且设置了点击“显示评论”才显示评论的功能。

我想把我的网站的评论也设置成平时隐藏，点击才显示的模式。于是在多说网站找到了[《动态加载多说评论框的方法》](http://dev.duoshuo.com/docs/50b344447f32d30066000147)的方法。

---

原来的"post.html"中的评论模块：

 <!-- 多说评论框 start -->

      <div class="comment">
           <div class="ds-thread" data-thread-key="{{page.id}}" data-title="{{page.title}}" data-url="{{site.url}}{{page.url}}">
           </div>
      </div>

<!-- 多说评论框 end -->

<!-- 多说公共JS代码 start (一个网页只需插入一次) -->

    <script type="text/javascript">
        var duoshuoQuery = {short_name:"cnfeat"};
        (function() {
        var ds = document.createElement('script');
        ds.type = 'text/javascript';ds.async = true;
        ds.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') + '//static.duoshuo.com/embed.js';
        ds.charset = 'UTF-8';
        (document.getElementsByTagName('head')[0]
         || document.getElementsByTagName('body')[0]).appendChild(ds);
        })();
    </script>

<!-- 多说公共JS代码 end -->

---

现在的评论模块：

<!-- 多说评论框 start -->

	<script>var duoshuoQuery =      {short_name:"qinpengblog"};</script>
    <script src="http://static.duoshuo.com/embed.js"></script>
				
	<script type="text/javascript">
				function toggleDuoshuoComments(container){
                         var el = document.createElement('div');//该div不需要设置class="ds-thread"
                             el.setAttribute('data-thread-key', '{{page.id}}');//必选参数
                             el.setAttribute('data-url', '{{site.url}}{{page.url}}');//必选参数
                             el.setAttribute('data-author-key', 'Peng');//可选参数
                             DUOSHUO.EmbedThread(el);
                             jQuery(container).append(el);
                }
     </script>
				
	<a href="javascript:void(0);" onclick="toggleDuoshuoComments('#comment-box');">显示评论</a>
    <div id="comment-box" ></div>	
		
<!-- 多说评论框 end -->

<!-- 多说公共JS代码 start (一个网页只需插入一次) -->

    <script type="text/javascript">
      var duoshuoQuery = {short_name:"qinpengblog"};
	    (function() {
		var ds = document.createElement('script');
		ds.type = 'text/javascript';ds.async = true;
		ds.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') + '//static.duoshuo.com/embed.js';
		ds.charset = 'UTF-8';
		(document.getElementsByTagName('head')[0] 
		 || document.getElementsByTagName('body')[0]).appendChild(ds);
	  })();
	</script>

<!-- 多说公共JS代码 end -->

目前的问题是，点击一次“显示评论”就多出一个评论框，即没有“收起评论”的功能。

---

走过的弯路：

刚开始直接把文章里面提到的代码插入"post.html",变成：

<!-- 多说评论框 start -->

    <a href="javascript:void(0);" onclick="toggleDuoshuoComments('#comment-box');">显示评论</a>

    <div id="comment-box" ></div>
                <div class="comment">
                    <div class="ds-thread" data-thread-key="{{page.id}}" data-title="{{page.title}}" data-url="{{site.url}}{{page.url}}">
                    </div>
                </div>

<!-- 多说评论框 end -->

<!-- 多说公共JS代码 start (一个网页只需插入一次) -->

    <script>var duoshuoQuery =      {short_name:"qinpengblog"};</script>
    <script src="http://static.duoshuo.com/embed.js"></script>

    <script type="text/javascript"> 
    var duoshuoQuery = {short_name:"qinpengblog"};
    (function() {
        var ds = document.createElement('script');
        ds.type = 'text/javascript';ds.async = true;
        ds.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') + '//static.duoshuo.com/embed.js';
        ds.charset = 'UTF-8';
        (document.getElementsByTagName('head')[0]
         || document.getElementsByTagName('body')[0]).appendChild(ds);
    })();

    function toggleDuoshuoComments(container){
                         var el = document.createElement('div');//该div不需要设置class="ds-thread"
                             el.setAttribute('data-thread-key', '{{page.id}}');//必选参数
                             el.setAttribute('data-url', '{{site.url}}{{page.url}}');//必选参数
                             el.setAttribute('data-author-key', 'Peng');//可选参数
                             DUOSHUO.EmbedThread(el);
                             jQuery(container).append(el);
     }
    </script>

<!-- 多说公共JS代码 end -->

结果效果仍是直接显示评论框，点击显示评论后，又蹦出来一个评论框。

删除掉：

    <div class="comment">
                    <div class="ds-thread" data-thread-key="{{page.id}}" data-title="{{page.title}}" data-url="{{site.url}}{{page.url}}">
                    </div>
    </div>

就没有默认显示的评论框了。

---










