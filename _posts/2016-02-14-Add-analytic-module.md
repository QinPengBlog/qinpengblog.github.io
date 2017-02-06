---
layout: post
title: 增加网站的统计分析模块并使网站可被搜索引擎索引
date: 2016-02-14 18:23
categories: blog
tags: [个人主页]
description: 记录增加的过程。

---

2016-07-10 18:16 Update

增加CNZZ统计功能。
添加以下代码在"Footer.html"中。

    <script type="text/javascript">var cnzz_protocol = (("https:" == document.location.protocol) ? " https://" : " http://");document.write(unescape("%3Cspan id='cnzz_stat_icon_1259876212'%3E%3C/span%3E%3Cscript src='" + cnzz_protocol + "s11.cnzz.com/z_stat.php%3Fid%3D1259876212%26show%3Dpic1' type='text/javascript'%3E%3C/script%3E"));
    </script>

之所以没有添加在以前的“head.html”中，是因为这个统计的方式是在页面上显示出元素，会影响页面效果。

---
_2016-02-17 11:25 更新_

我的网站已经被Google抓取了。

<Center>
![Google Console](http://7xqvz5.com1.z0.glb.clouddn.com/image%2FGoogle%20Console.png)
</center>

<center>Google Concole 通知</center>

在Google上的搜索结果：

<center>![](http://7xqvz5.com1.z0.glb.clouddn.com/image%2FGoogle%20Search.png)
</center>

<center>Google Search Result</center>

---

想要记录多少人访问了我的网站，所以一番搜索，找到了几个流量统计的站点。最后选择了Google和Baidu结合的方式。因为Google的统计分析内容丰富，但是据说会有延迟，而Baidu不会有延迟。

参考:

- [《Setting up this blog site: github, jekyll, and the hpstr theme》](http://nicolaroberts.github.io/website-setup-post/)

- [《利用github-pages建立个人博客》](http://coolshell.info/blog/2015/03/github-pages-blog.html)

- [Verify site ownership on Google Search Console](https://support.google.com/analytics/answer/1142414?hl=en)

- [Verify your site ownership](https://support.google.com/webmasters/answer/35179?hl=en)

将Google analytics 和Google verify在"_config.yml"中设置如下：

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

并在/_includes/增加"Baidu"文件夹，然后建立"analytics"文件。参考文章的方法，加入百度统计的代码。

测试结果是百度统计检测不到代码，google和bing无法认证。

---

猜测可能google和bing的认证是通过content里的内容，所以修改代码成：

    <# Analytics and webmaster tools stuff goes here
    analytics :
      provider : Baidu
    google_analytics: UA-73781127-1
    google_verify: f-xallGRfKu4KN9VgwJYGRZprRAHyGPUIIz6O4A9Yck />
    # https://ssl.bing.com/webmaster/configure/verify/ownership Option 2 content= goes here
    bing_verify: 731D1E6005EE00E5770F4B5909254F51 />
    />

仍然无法认证。

---

保留"_config.yml"中的代码，将百度统计代码和两处的认证代码放在/_includes/head.html中：

	<!--Verify Begin-->
	<meta name="google-site-verification" content="f-xallGRfKu4KN9VgwJYGRZprRAHyGPUIIz6O4A9Yck" />
	<meta name="msvalidate.01" content="731D1E6005EE00E5770F4B5909254F51" />
	<!--Verify END-->
	
	<!--Analysis Begin-->
	<script>
		var _hmt = _hmt || [];
			(function() {
				var hm = document.createElement("script");
					hm.src = "//hm.baidu.com/hm.js?4009ddf30ad4a3d26d3f86f0d12a1c1a";
					var s = document.getElementsByTagName("script")[0]; 
					s.parentNode.insertBefore(hm, s);
		})();
	</script>
	<!--Analysis END-->

结果认证全部成功，统计代码测试成功。

---

之后在www.xml-sitemaps.com上认证域名qinpeng.space，生成"sitemaps.xml"，上传到我的网站的根目录。然后将qinpeng.space/sitemaps.xml登记到google和bing中。
> 应该是不需要再认证www.qingpeng.space，根目录只能上传一个；google需要连接带www和不带www的域名。

浏览Google analysis的选项的时候，发现可以发出测试流量，尝试后发现实时显示了出来。想起我没有在head.html中添加google analysis的代码，不知道是meta认证的代码通过连接起了作用，还是"_config.yml"中的代码起了作用。

---










