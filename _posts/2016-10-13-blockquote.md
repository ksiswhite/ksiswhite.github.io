---
layout: post
title: "CSS&HTML:关于<blockquote>标签自动换行以及<a>标签新窗口打开"
date:   2016-10-12
excerpt: "通过修改CSS文件，使<blockquote>标签实现自动换行，通过添加属性使<a>标签实现链接新窗口打开"
tag:
- CSS
- HTML
---
<p>　　在写前一条博客的神秘代码的时候，发现在&lt;blockquote&gt;标签内，未实现自动换行，神秘代码就一大长串的在一行内显示，简直不能忍，所以就搜索了一下解决方案，找到了这个:</p>
<blockquote>
<p>blockquote{<br>  　　margin:0;<br>  　　padding:0;<br>  　　border:0;<br>  　　font:inherit;<br>  　　font-size:100%;<br>  　　<strong>white-space: pre-wrap;      /* css-3 */</strong><br>  　　<strong>white-space: -moz-pre-wrap !important;  /* Mozilla, since 1999 */</strong><br>  　　<strong>white-space: -pre-wrap;      /* Opera 4-6 */</strong><br>  　　<strong>white-space: -o-pre-wrap;    /* Opera 7 */</strong><br>  　　<strong>word-wrap:break-word;    /* ie */</strong><br>  　　<strong>overflow:hidden;</strong><br>  　　vertical-align:baseline<br>}</p>
</blockquote>
<p>　　在CSS代码中加入如上几行代码即可解决！</p>
<p>　　关于&lt;a&gt;标签实现新窗口打开，只需要加入target=&quot;_blank&quot;即可。</p>
