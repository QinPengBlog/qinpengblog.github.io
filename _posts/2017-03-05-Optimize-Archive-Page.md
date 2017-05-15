---
layout: post
title: 优化Archive页面
date: 2017-03-03
categories: blog
tags: [Blog]
description: 
---

年份分割设为标题样式`<h3>{{ y }}</h3>`

年份分隔去掉无序排列标记
`<li class="listing-seperator">{{ y }}</li>`
改为
`{{ y }}`

---

原来：

```
---
layout: page
title: "Archive"
description: "你看到的，是我之为我的原因"
header-img: "img/orange.jpg"
---

<ul class="listing">
{% for post in site.posts %}
  {% capture y %}{{post.date | date:"%Y"}}{% endcapture %}
  {% if year != y %}
    {% assign year = y %}
    <li class="listing-seperator">{{ y }}</li>
  {% endif %}
  <li class="listing-item">
    <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
    <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
  </li>
{% endfor %}
</ul>
```

---










