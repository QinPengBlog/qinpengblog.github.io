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



---

