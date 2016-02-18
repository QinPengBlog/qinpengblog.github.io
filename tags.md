---
layout: page
title: "Tags"
description: "啊，被你发现了我的精神遗传物质"  
header-img: "img/semantic.jpg"  
---

## 本页使用方法

1. 在下面选一个你喜欢的词
2. 点击它
3. 相关的文章会「唰」地一声射到页面顶端
4. 马上试试？

## 遗传列表

Test12

{% assign tags = site.tags | sort %}
{% for tag in tags %}
 <span class="site-tag">
   <a href="/tag/{{ tag | first | slugify }}/"
   style="font-size: {{ tag | last | size  |  times: 4 | plus: 80  }}%">{{ tag[0] | replace:'-', ' ' }} ({{ tag | last | size }})</a>
 </span>
{% endfor %}

---
Test11

<div>
  {% include tag_cloud %}
  <div class='clear'></div>
</div>

---
Test10

<div class="tag-cloud">
   {% for tag in site.tags %}
   <a href="#posts-tag" id="{{ forloop.index }}" class="__tag" style="margin: 5px">{{ tag[0] }}</a>
   <ul id="list_{{ forloop.index }}" style="display:none;">
   {% for post in tag[1] %}
   <li><a href="{{ post.url }}">{{ post.title }}</a></li>
   {% endfor %}

   </ul>
   {% endfor %}
</div>

<div id ="posts-tags" class="post-list" style="margin: 50px;"></div>

<script type="text/javascript">
  $(function() {
   var minFont = 15.0,
   maxFont = 40.0,
   diffFont = maxFont - minFont,
   size = 0;
       
   {% assign max = 1.0 %}

   {% for tag in site.tags %}
   {% if tag[1].size > max %}
   {% assign max = tag[1].size %}
   {% endif %}
   {% endfor %}
            
   {% for tag in site.tags %}
   size = (Math.log({{ tag[1].size }}) / Math.log({{ max }})) * diffFont + minFont;
   $("#{{ forloop.index }}").css("font-size", size + "px");
   {% endfor %}

   $('.tag-cloud a[class^="__tag"]').click(function() {
   $('.post-list').empty();
   $('#list_' + $(this).attr('id')).each(function() {
   $('.post-list').append('<ul>' + $(this).html() + '</ul>');
   });
   });
   });
</script>

---
Test9

<link rel="stylesheet" type="text/css" href="/css/jqcloud.css" />
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.4.4/jquery.js"></script>
<script type="text/javascript" src="/js/jqcloud-1.0.4.js"></script>

<script type="text/javascript">
   var word_array = [
   {% for tag in site.tags %}
   {text: "{{ tag[0] }}", weight: 13, link:"#{{ tag[0] }}"},
   {% endfor %}
   {text: "Lorem", weight: 15}
  ];
$(function() {
   $("#tagsss").jQCloud(word_array);
});
</script>

<div id="tagsss" style="width: 550px; height: 350px;"></div>

---
Test8

<script type="text/javascript" src="/js/jquery.tagcloud.js"></script> 

<div id="tagscloud">
{% for tag in site.tags %}
<a href="#{{ tag[0] }}" title="{{ tag[0] }}" rel="{{ tag[1].size }}">{{ tag[0] }}</a>
{% endfor %}
</div>

<script language="javascript">
$.fn.tagcloud.defaults = {
   size: {start: 14, end: 18, unit: 'pt'},
   color: {start: '#cde', end: '#f52'}
   };
$(function () {
   $('#tagscloud a').tagcloud();
   });
</script>

---

<!--列出每个tag出现的文章-->

<ul class="listing">
{% for tag in site.tags %}
  <li class="listing-seperator" id="{{ tag[0] }}"><h4>{{ tag[0] }}</h4> <h8><a><span>{{ tag[0].size }}</span></a></h8></li>

  {% for post in tag[1] %}
  <li class="listing-item">
  <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
  <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
  </li>
  {% endfor %}

<hr>

{% endfor %}
</ul>

---