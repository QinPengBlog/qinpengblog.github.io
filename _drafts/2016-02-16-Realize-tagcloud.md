<div id="whatever">
      <a href="/path" rel="7">peace</a>
      <a href="/path" rel="3">unity</a>
      <a href="/path" rel="10">love</a>
      <a href="/path" rel="5">having fun</a>
</div>


$.fn.tagcloud.defaults = {
      size: {start: 14, end: 18, unit: 'pt'},
      color: {start: '#cde', end: '#f52'}
    };

$(function () {
      $('#whatever a').tagcloud();
    });

原来：

<script src="/media/js/jquery.tagcloud.js" type="text/javascript" charset="utf-8"></script> 
<script language="javascript">
$.fn.tagcloud.defaults = {
    size: {start: 1, end: 1, unit: 'em'},
      color: {start: '#f8e0e6', end: '#ff3333'}
};

$(function () {
    $('#tag_cloud a').tagcloud();
});
</script>

发现没有/media/js/jquery.tagcloud.js这个文件，我用我拷贝的jquery.tagcloud.js代替，改成：

<script src="/js/jquery.tagcloud.js" type="text/javascript" charset="utf-8"></script> 
<script language="javascript">
$.fn.tagcloud.defaults = {
    size: {start: 1, end: 1, unit: 'em'},
      color: {start: '#f8e0e6', end: '#ff3333'}
};

$(function () {
    $('#tag_cloud a').tagcloud();
});
</script>

没有变化。想到以前本没有文件的时候也没有效果。

尝试删掉这段：

<script src="/js/jquery.tagcloud.js" type="text/javascript" charset="utf-8"></script> 
<script language="javascript">
$.fn.tagcloud.defaults = {
    size: {start: 1, end: 1, unit: 'em'},
      color: {start: '#f8e0e6', end: '#ff3333'}
};

$(function () {
    $('#tag_cloud a').tagcloud();
});
</script>

果然没有变化。

##Test1

用原来的代码：


<div id='tag_cloud'>
{% for tag in site.tags %}
<a href="#{{ tag[0] }}" title="{{ tag[0] }}" rel="{{ tag[1].size }}">{{ tag[0] }}</a>
{% endfor %}
</div>

替代Demo里的代码的第一部分：

<div id="whatever">
      <a href="/path" rel="7">peace</a>
      <a href="/path" rel="3">unity</a>
      <a href="/path" rel="10">love</a>
      <a href="/path" rel="5">having fun</a>
</div>

用Demo里的代码的第二部分：

$.fn.tagcloud.defaults = {
      size: {start: 14, end: 18, unit: 'pt'},
      color: {start: '#cde', end: '#f52'}
    };

$(function () {
      $('#whatever a').tagcloud();
    });

替代原来代码的最后一部分的相应代码：

<script src="/js/jquery.tagcloud.js" type="text/javascript" charset="utf-8"></script> 

<script language="javascript">
$.fn.tagcloud.defaults = {
      size: {start: 14, end: 18, unit: 'pt'},
      color: {start: '#cde', end: '#f52'}
    };

$(function () {
      $('#tag_cloud a').tagcloud();
    });
</script>

Nothing happened.

P.S.为了识别出Github已经编译了新上传的文件，在文件中添加了test文字。

##Test2

猜测是不是因为MD文件中编译的时候不那个直接读取html语言。

<html>
<div id='tag_cloud'>
{% for tag in site.tags %}
<a href="#{{ tag[0] }}" title="{{ tag[0] }}" rel="{{ tag[1].size }}">{{ tag[0] }}</a>
{% endfor %}
</div>
</html>

<html>
<script src="/js/jquery.tagcloud.js" type="text/javascript" charset="utf-8"></script> 

<script language="javascript">
$.fn.tagcloud.defaults = {
      size: {start: 14, end: 18, unit: 'pt'},
      color: {start: '#cde', end: '#f52'}
    };

$(function () {
      $('#tag_cloud a').tagcloud();
    });
</script>
</html>

Nothing happened.

P.S.发现About，Tags等页面均不把markdown标识编译出来，而是直接显示##。

## Test3

Open page.html to study.

Move:
type="text/javascript"
to the front of src.

Delete:
charset="utf-8"

把第三段代码移动到第一段之中：


<html>
<script type="text/javascript" src="/js/jquery.tagcloud.js"></script> 

<div id='tag_cloud'>
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
      $('#tag_cloud a').tagcloud();
    });
</script>

</html>

Nothing happened.

## Test4

还是怀疑是代码执行的问题，Google“如何在markdown中执行html代码”。在知乎中找到一个[回答](https://www.zhihu.com/question/19963642/answer/16025634)。结论是不需要< html>< /html>。

>著作权归作者所有。
商业转载请联系作者获得授权，非商业转载请注明出处。
作者：潘韬
链接：https://www.zhihu.com/question/19963642/answer/16025634
来源：知乎
Markdown 语法进阶在 Markdown 中嵌入原生HTML代码在 Markdown 代码中嵌入 HTML代码，如果你想直接在 Markdown 中嵌入HTML代码，那么你只需要将代码直接写在需要的地方即可：这是一个段落。
    <table>
    <tr>
        <td>这是用原生的HTML代码写的表格。</td>
    </tr>
    </table>
这是另一个段落。

>转换之后得到：
    <p>这是一个段落。</p>
    <table>
    <tr>
        <td>这是用原生的HTML代码写的表格。</td>
    </tr>
    </table>
    <p>这是另一个段落。</p>

## Test5

隐藏标签云相关代码：

发现确实被隐藏了，而后面的每个标签出现的文章列表没有受到影响。

    <!--Tagcloud
    <script type="text/javascript" src="/js/jquery.tagcloud.js"></script> 

    <div id='tag_cloud'>
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
      $('#tag_cloud a').tagcloud();
    });
	</script>
	-->

Test6

发现代码里和说明文档里面不一样的地方：

    <div id='tagscloud'>

应该是双引号：

    <div id="whatever">

Nothing happened.

## Test7

find that:

img="img/**.jpg" 

maybe the src is not right:

    <script type="text/javascript" src="/js/jquery.tagcloud.js"></script> 

change it to:

	<script type="text/javascript" src="js/jquery.tagcloud.js"></script> 

## Test8

It seems that '/js/jquery.tagcloud.js' following src, rather than "/js/jquery.tagcloud.js".

    <script type="text/javascript" src='/js/jquery.tagcloud.js'></script> 

STILL NOTHING HAPPENED.

### Test8+

Add"---"after the tag cloud. Done.

### Test8++

Add "---" to each tag in the list part. Only show as ---.
As the "---" is in html part, so Google to find that < hr> represent horizental rule. Change the "---" to < hr>. 

    <ul class="listing">
	{% for tag in site.tags %}
  	<li class="listing-seperator" id="{{ tag[0] }}">{{ tag[0] }}</li>
	{% for post in tag[1] %}
  	<li class="listing-item">
  	<time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
  	<a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
  	</li>
	{% endfor %}
	<hr>
	{% endfor %}
	</ul>

Done. 

The problem now is how to cancel the unorder list before each tag.

### Test8+++

Stand out the tags by adding < h3>< /h3>.

	 <li class="listing-seperator" id="{{ tag[0] }}"><h3>{{ tag[0] }}</h3></li>

Done.

change h3 to h4


### Test9

Use [jQCloud](https://github.com/lucaong/jQCloud)。

	<link rel="stylesheet" type="text/css" href="/css/jqcloud.css" />
	<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.4.4/jquery.js"></script>
	<script type="text/javascript" src="/js/jqcloud-1.0.4.js"></script>

	<script type="text/javascript">
   		var word_list = [
   		{% for tag in site.tags %}
   		{text: "{{ tag[0] }}", weight: 2, link:"#{{ tag[0] }}"},
   		{% endfor %}
  		];
	$(function() {
	   	$("#my_favorite_latin_words").jQCloud(word_list, {shape: "rectangular"});
	});
	</script>

	<div id="my_favorite_latin_words" style="width: 550px; height: 350px; border: 1px solid #ccc;"></div>

出现了一个空白的长方形···里面并没有tags。

change the word_list to word_array according to readme.md。

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

Nothing happened.

## Test10

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

Only list the tags.

## Test11

[Create a tag cloud using Jekyll](http://diydeveloper.io/tech/2014/03/09/create-a-tag-cloud-in-jekyll/)

In /_includes/JB folder, create a new file called “tag_cloud”.

Copy and paste this into the file:

	{% comment %}
	Creates a tag cloud on your page.
	{% endcomment %}

	{% for tag in site.tags %}
  	<span class="tag-cloud-{{ tag | last | size | times: 10 | divided_by: site.tags.size }}">
  	<a href="{{ BASE_PATH }}{{ site.JB.tags_path }}#{{ tag | first | slugize] }}-ref">{{ tag | first }}</a>
  	</span>
	{% endfor %}

Add the code below to the end of clean-blog.css

	/* tag cloud */
	.tag-cloud-0 { font-size: 1em; }
	.tag-cloud-1 { font-size: 1.5em; }
	.tag-cloud-2 { font-size: 1.5em; font-weight: bold; }
	.tag-cloud-3 { font-size: 2em; }
	.tag-cloud-4 { font-size: 2em; font-weight: bold; }
	.tag-cloud-5 { font-size: 2.5em; }
	.tag-cloud-6 { font-size: 2.5em; font-weight: bold; }
	.tag-cloud-7 { font-size: 2.75em; }
	.tag-cloud-8 { font-size: 2.75em; font-weight: bold; }
	.tag-cloud-9 { font-size: 2.75em; font-weight: bold; font-style: italic; }
	.tag-cloud-10 { font-size: 3em; }
	/* end tag cloud */

Add the code below to Tags.md

	<div>
	<h2 class='title'>Tag Cloud</h2>
	{% include JB/tag_cloud %}
	<div class='clear'></div>
	</div>

Informed by Github that failed to build the page:

> A file was included in `tags.md` that is a symlink or does not exist in your `_includes` directory. For more information, see 
> 
> https://help.github.com/articles/page-build-failed-file-is-a-symlink.
> 
> GitHub Pages was recently upgraded to Jekyll 3.0. It may help to confirm you're using the correct dependencies:
> 
> https://github.com/blog/2100-github-pages-now-faster-and-simpler-with-jekyll-3-0

> Troubleshooting a symlinked file error

> We strongly recommend running Jekyll locally so you can easily debug and fix build errors before pushing to GitHub.
> 
> 1. Use your favorite text editor to open the file mentioned in the build failure email.

> 2. Search for the include tag to see where you've referenced other files. For example: {% include cool_header.html %}.

> 3. Copy or move any symlinked files into the _includes directory of your GitHub Pages repository.

> 4. Commit and push to your GitHub Pages repository on GitHub to trigger another build on the server.

Try to add a "/" to fix it.

	<div>
	<h2 class='title'>Tag Cloud</h2>
	{% include /JB/tag_cloud %}
	<div class='clear'></div>
	</div>

Not help.

### Test11++

Move tag_cloud to _includes folder.

	<div>
	<h2 class='title'>Tag Cloud</h2>
	{% include tag_cloud %}
	<div class='clear'></div>
	</div>

It works! The tag "个人主页" was bigger than other tags.

### Test11+++

But when you click on a tag, it doesn't go to the tag list. So I check the code and url appears after clicking on the tag, then I modify the code in tag_cloud by deleting "-ref".

	{% comment %}
	Creates a tag cloud on your page.
	{% endcomment %}

	{% for tag in site.tags %}
  	<span class="tag-cloud-{{ tag | last | size | times: 10 | divided_by: site.tags.size }}">
  	<a href="{{ BASE_PATH }}{{ site.JB.tags_path }}#{{ tag | first | slugize] }}">{{ tag | first }}</a>
  	</span>
	{% endfor %}

Yeah, it works.

### Test11++++

Want to show the number of the posts containing the tags. Learn from:

{% for tag in site.tags %}
  <a class="tag-anchor" id="{{ tag[0] }}-ref"></a>
  <h3 class="tag_box">{{ tag[0] }} <a><span>{{ tag[0].size }}</span></a></h3>
  <ul>
    {% assign pages_list = tag[1] %}
    {% include JB/pages_list %}
  </ul>
{% endfor %}

Just add <a><span>{{ tag[0].size }}</span></a>

	  <li class="listing-seperator" id="{{ tag[0] }}"><h4>{{ tag[0] }} <a><span>{{ tag[0].size }}</span></a></h4></li>

Find that the tag.size stands for the number of posts containing this tag. 

But the style of the number is not well as it is same to tag, which may confuse readers. Need to custom the style of the number.

---

## Test12

[Generating Tag cloud on Jekyll blog without plugin
](https://superdevresources.com/tag-cloud-jekyll/)

{% assign tags = site.tags | sort %}
{% for tag in tags %}
 <span class="site-tag">
   <a href="/tag/{{ tag | first | slugify }}/"
   style="font-size: {{ tag | last | size  |  times: 4 | plus: 80  }}%">{{ tag[0] | replace:'-', ' ' }} ({{ tag | last | size }})</a>
 </span>
{% endfor %}

It works. But the tags showing up in a list.

Find Test10 works now.

### Test12+
Change the link of the tags to #{{ tag[0] }} in Test10 and 12. But when I click on the tags in Test10, I find the previous link towards to show up the relating posts below the tags. It is a different showing up way, so I keep it. Only change in Test12. The previous links of the tags in Test12 towards http://qinpeng.space/tag/{{tag[]}}/.



---

## To-do list

- Need to search "Tag" in jekyll to get to know the related things.

- Learn html, Javascript systematically.

- Custom the style of the number of tag. 

- 

---

