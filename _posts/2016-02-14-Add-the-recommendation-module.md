---
layout: post
title: 增加网站的推荐模块
date: 2016-02-13
categories: blog
tags: [个人主页]
description: 记录增加的过程。

---

多说的分享模块不够好，无意中发现[JiaThis](http://www.jiathis.com/)，感觉不错。在主页下面发现了[友荐](http://www.ujian.cc/)，感觉不错，想给我的网站加上这个功能。

友荐为PC端提供4中推荐方式：侧栏式，嵌入式，双栏式和边栏式。

- 侧栏式：侧栏式滑动切入在页面右（左）下角，不影响页面布局。
> 可以设置个数（1-10），位置（左侧，右侧），附赠返回顶部按钮。P.S. 感觉像小广告似的，不取。

- 嵌入式：嵌入式使用范围最广，多出现在网页正文下方，直观凸显推荐内容，增加用户浏览粘性。
> 可以设置个数（1-18），显示方式（上图下文，左图右文，文字，智能），行数（1-5）等等。P.S. 太占地，广告色彩较多。

- 双栏式：双栏式配合多文字类型页面使用，形式简介明了，符合用户的浏览行为。
> 可以设置个数（2,4,6,8,10），显示方式（双列图文or双列文字）。

- 边栏式：边栏式多应用于专题活动或新闻资讯正文侧边栏板块，增强的曝光与推广。
> 可以设置个数（2,4,6,8,10,12,14）。P.S. 赤裸裸的小广告呀。

最后选择了双栏文字式，显示6条文字推荐，设置了鼠标滑过的模块和文本颜色，打开内容链接的方式为新窗口。

代码如下：

<!-- UJian Button BEGIN -->
                <div class="ujian-hook"></div>
                <script type="text/javascript">var ujian_config = {num:6,showType:4,lkrc:4,target:1,bgColor:'#',hoverTextColor:'#116BF2'};</script>
                <script type="text/javascript" src="http://v1.ujian.cc/code/ujian.js?uid=2083931"></script>
                <a href="http://www.ujian.cc" style="border:0;"><img src="http://img.ujian.cc/pixel.png" alt="友荐云推荐" style="border:0;padding:0;margin:0;" /></a>
<!-- UJian Button END -->

关于友荐的更多内容请移步[友荐帮助中心](http://www.ujian.cc/help/index/)

---










