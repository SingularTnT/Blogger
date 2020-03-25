---
title: ''
---

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/Blogger_icon_2017.svg.png" width="15%">
</div>

这篇博文介绍了在Blogger中如何分隔摘要和正文，针对Markdown写作生成HTML
的方式。</br>
<!-- more -->

<meting-js
	server="netease"
	type="song"
	id="188647">
</meting-js>

**TOC**

<!-- TOC -->

- [1. 关于Blogger的摘要](#1-关于blogger的摘要)
- [2. 关于Blogger的摘要](#2-关于blogger的摘要)
- [参考(References)](#参考references)

<!-- /TOC -->

<a id="markdown-1-关于blogger的摘要" name="1-关于blogger的摘要"></a>
## 1. 关于Blogger的摘要

******

在Blogger主页的排版中，会默认自动展示博文的缩略图以及摘要内容。而由于我习惯通过Markdown写作生成HTML进行发布的方式，Blogger会自动把文章中一段固定长度的内容作为摘要进行展示，比如这篇博文：

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/zhaiyao1.png" width="100%">
</div>

在主页展示出来的效果：

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/zhaiyao2.png" width="100%">
</div>

可以看出来很乱，由于摘要部分的字数比较少，自动展示的内容把TOC和正文也加进去了。

**Tips**：在摘要底下加几个`</br>`标签也可以，但并不是一个完美的方案。

<a id="markdown-2-关于blogger的摘要" name="2-关于blogger的摘要"></a>
## 2. 关于Blogger的摘要

******

参照Blogger官方的博客说明，可以插入"Jump Breaks"以分隔摘要和正文内容，在博文的"撰写"模式下，可以直接插入分隔符：

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/zhaiyao3.png" width="100%">
</div>

而当我们通过生成的HTML上传时，"撰写"页面是空白的，因此最方便的方式是在Markdown中插入`<!-- more --> `标记即可，类似如下形式即可：

```markdown
摘要:xxx

<!-- more -->

正文:xxx
```

生成的HTML文件也会带上"Jump Breaks"分隔符。

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/zhaiyao4.png" width="100%">
</div>

保存更新后的最终效果：

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/zhaiyao5.png" width="100%">
</div>

可以看出非常好的展示了所需要的内容，而不会带上多余的TOC或者正文等。

<a id="markdown-参考references" name="参考references"></a>
## 参考(References)

******

* [You Might As Well Jump!](https://blogger.googleblog.com/2009/09/you-might-as-well-jump.html) </br>


<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>