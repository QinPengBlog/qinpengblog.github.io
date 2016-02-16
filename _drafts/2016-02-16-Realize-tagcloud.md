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

##Test3

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


---

