---
layout: post
title: 增加网站的推荐模块
date: 2016-02-14
categories: blog
tags: [个人主页]
description: 记录增加的过程。

---

多说的分享模块不够好。

无意中发现[JiaThis](http://www.jiathis.com/)，感觉不错。吸引我的几点是：自定义功能强大，具有智能排序功能，数据统计功能强大。

[《选择JiaThis的八大理由》](http://www.jiathis.com/help/html/why-choose-jiathis)

[《一般安装到网站哪里?》](http://www.jiathis.com/help/html/where-install-jiathis)

##JiaThis

JiaThis分享按钮的几种方式：侧栏式，工具式，图标式，边栏式，喜欢按钮，按钮式，关注按钮，图片分享，划词分享。

- 侧栏式：隐藏在侧栏。
- 工具式：同多说的分享模块。
- 图标式：与工具式相比，少了图标的文字说明。
- 边栏式：悬浮在文章边。
- 按钮式：只有一个按钮。
- 图片分享：用户将鼠标移动到指定的图片上时，分享按钮就会出现。
- 划词分享：任意划取部分文字信息（＞5个字），即可显示JiaThis划词分享图标。
- 喜欢按钮：喜欢的同时进行分享。
- 关注按钮：转到对应社交账号主页。
 
选择图标式，图片分享和划词分享。

###图标式：

<!-- JiaThis Button BEGIN -->

				<div class="jiathis_style">
					<a class="jiathis_button_weixin"></a>
					<a class="jiathis_button_tsina"></a>
					<a class="jiathis_button_pocket"></a>
					<a class="jiathis_button_instapaper"></a>
					<a class="jiathis_button_copy"></a>
					<a href="http://www.jiathis.com/share?uid=2083931" class="jiathis jiathis_txt jiathis_separator jtico jtico_jiathis" target="_blank"></a>
					<a class="jiathis_counter_style"></a>
				</div>
				<script type="text/javascript" >
					var jiathis_config={
						data_track_clickback:true,
						summary:"",
						shortUrl:true,
						hideMore:false
					}
				</script>
				<script type="text/javascript" src="http://v3.jiathis.com/code_mini/jia.js?uid=2083931" charset="utf-8"></script>

<!-- JiaThis Button END -->

###图片分享

官方说明：如果您的网页中已经嵌入jia.js或jiathis_r.js，只需将以下绿色部分代码复制到JiaThis分享代码之前即可。

<!-- JiaThis Picture BEGIN -->

	<script type="text/javascript">
		 var jiathis_config = {
			shareImg:{
			"showType":"ALL",
			"bgColor":"",
		    "txtColor":"",
			"text":"",
			"services":"",
			"position":"",
			"imgwidth":"",
			"imgheight":"",
			"divname":""
		    }
		 }
	</script>

<!-- JiaThis Picture END -->

JiaThis分享代码是：

    <script type='text/javascript' src='http://v3.jiathis.com/code/jia.js?uid=2083931' charset='utf-8'></script>

因为图标式代码中含有JiaThis分享代码，所以尝试的时候是把图片分享的代码插入到了图标式代码中间：

<!-- JiaThis Button BEGIN -->

				<div class="jiathis_style">
					<a class="jiathis_button_weixin"></a>
					<a class="jiathis_button_tsina"></a>
					<a class="jiathis_button_pocket"></a>
					<a class="jiathis_button_instapaper"></a>
					<a class="jiathis_button_copy"></a>
					<a href="http://www.jiathis.com/share?uid=2083931" class="jiathis jiathis_txt jiathis_separator jtico jtico_jiathis" target="_blank"></a>
					<a class="jiathis_counter_style"></a>
				</div>
				<script type="text/javascript" >
					var jiathis_config={
						data_track_clickback:true,
						summary:"",
						shortUrl:true,
						hideMore:false
					}
				</script>
				<script type="text/javascript" src="http://v3.jiathis.com/code_mini/jia.js?uid=2083931" charset="utf-8"></script>

<!-- JiaThis Picture BEGIN -->

	<script type="text/javascript">
		 var jiathis_config = {
			shareImg:{
			"showType":"ALL",
			"bgColor":"",
		    "txtColor":"",
			"text":"",
			"services":"",
			"position":"",
			"imgwidth":"",
			"imgheight":"",
			"divname":""
		    }
		 }
	</script>

<!-- JiaThis Picture END -->

<!-- JiaThis Button END -->

结果没有显示，遂删掉这个模块。

###划词分享：

官方说明：用户为网站页面添加划词分享时，需要为想开放划词分享的页面div框架添加 class="jiathis_streak"。如：< div class="jiathis_streak">< /div>或< div class="site_main jiathis_streak">< /div>。

最开始是把这行代码放在前面：

<!-- JiaThis 划词分享 BEGIN -->

                <div class="jiathis_streak"></div>

                <div class="jiathis_streak_share_16x16" id="jiathis_streak_share" style="display:none">
					<span class="streak_share_jiao"></span>
					<div class="jiathis_streak_goshare" id="jiathis_streak_goshare">
						<span class="jiathis_streak_txt">分享到</span>  
						<span style="" title="隐藏分享框" onclick="JIATHIS_STREAK.hideShare()" class="jiathis_streak_close">X</span>
					</div>
					<div class="jiathis_style" >
						<a class="jiathis_button_tsina"></a>
						<a class="jiathis_button_weixin"></a>
						<a class="jiathis_button_twitter"></a>
						<a class="jiathis_button_translate"></a>
						<a class="jiathis_button_ydnote"></a>
						<a href="http://www.jiathis.com/share" class="jiathis jiathis_txt jtico jtico_jiathis" target="_blank"></a>
						<script type="text/javascript">
							var jiathis_config = {data_track_clickback:'true'};
						</script>
						
						<script type="text/javascript" src="http://v3.jiathis.com/code/jia.js?uid=2083931" charset="utf-8"></script>	
						<script type="text/javascript" src="http://v3.jiathis.com/code/jiathis_streak.js" charset="utf-8"></script>
					</div>
				</div>

<!-- JiaThis 划词分享 END -->

结果没有作用。考虑到可能是要把后面的代码放到jiathis_streak的Div域中，改成了下面的形式：

<!-- JiaThis 划词分享 BEGIN -->

			    <div class="jiathis_streak">

                <div class="jiathis_streak_share_16x16" id="jiathis_streak_share" style="display:none">
					<span class="streak_share_jiao"></span>
					<div class="jiathis_streak_goshare" id="jiathis_streak_goshare">
						<span class="jiathis_streak_txt">分享到</span>  
						<span style="" title="隐藏分享框" onclick="JIATHIS_STREAK.hideShare()" class="jiathis_streak_close">X</span>
					</div>
					<div class="jiathis_style" >
						<a class="jiathis_button_tsina"></a>
						<a class="jiathis_button_weixin"></a>
						<a class="jiathis_button_twitter"></a>
						<a class="jiathis_button_translate"></a>
						<a class="jiathis_button_ydnote"></a>
						<a href="http://www.jiathis.com/share" class="jiathis jiathis_txt jtico jtico_jiathis" target="_blank"></a>
						<script type="text/javascript">
							var jiathis_config = {data_track_clickback:'true'};
						</script>
						
						<script type="text/javascript" src="http://v3.jiathis.com/code/jia.js?uid=2083931" charset="utf-8"></script>	
						<script type="text/javascript" src="http://v3.jiathis.com/code/jiathis_streak.js" charset="utf-8"></script>
					</div>
				</div>
			  </div>

<!-- JiaThis 划词分享 END -->

但是仍然不起作用，遂删掉这个模块。

---

原来的多说的分享代码：

<!-- Duoshuo Share start -->

                <style>
                    .ds-share{
                        text-align: right;
                    }
                    
                    @media only screen and (max-width: 700px) {
                        .ds-share {

                        }
                    }
                </style>

                <div class="ds-share"
                    data-thread-key="{{page.id}}" data-title="{{page.title}}"
                    data-images="{{ site.url }}/{% if page.header-img %}{{ page.header-img }}{% else %}{{ site.header-img }}{% endif %}"
                    data-content="{{ content | strip_html | truncate:80 }} | Microdust:Azeril's blog"
                    data-url="{{site.url}}{{page.url}}">
                    <div class="ds-share-inline">
                      <ul  class="ds-share-icons-16">

                        <li data-toggle="ds-share-icons-more"><a class="ds-more" href="#">分享到：</a></li>
                        <li><a class="ds-wechat flat" href="javascript:void(0);" data-service="wechat">微信</a></li>
                        <li><a class="ds-weibo flat" href="javascript:void(0);" data-service="weibo">微博</a></li>
                        <li><a class="ds-douban flat" href="javascript:void(0);" data-service="douban">豆瓣</a></li>
                      </ul>
                      <div class="ds-share-icons-more">
                      </div>
                    </div>
                <hr>
                </div>

<!-- Duoshuo Share end-->








