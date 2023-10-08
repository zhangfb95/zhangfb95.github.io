---
layout: page
title: "Tags"
description: "哈哈，你找到了我的文章标签列表"  
header-img: "img/Red-Brown.jpg"  
---

## 本页使用方法

1. 在下面选一个你喜欢的词
2. 点击它
3. 相关的文章会「唰」地一声跳到页面顶端
4. 马上试试？

## 标签总览

<div id='tag_cloud'>| 
{% for tag in site.tags %}
<a href="#{{ tag[0] }}" title="{{ tag[0] }}" rel="{{ tag[1].size }}">{{ tag[0] }}</a> | 
{% endfor %}
</div>

## 标签列表

{% for tag in site.tags %}
#### {{ tag[0] }}
{% for post in tag[1] %}
1. {{ post.date | date:"%Y-%m-%d" }}[{{ post.title }}]({{ post.url }})
{% endfor %}
{% endfor %}

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
