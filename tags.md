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

{% for tag in site.tags %}
   <a href="#{{ tag[0] }}"
        style="font-size: {{ tag | last | size  |  times: 4 | plus: 80  }}%">{{ tag[0] | replace:'-', ' ' }} ({{ tag | last | size }})
   </a>
{% endfor %}

---

<div>
  {% include tag_cloud %}
  <div class='clear'></div>
</div>

---

<!--列出每个tag出现的文章-->

<ul class="listing">
{% for tag in site.tags %}
  <h4>{{ tag[0] }}<a><span>{{ tag[0].size }}</span></a></h4>

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