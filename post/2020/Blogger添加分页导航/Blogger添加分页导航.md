---
title: ''
---

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/Blogger_icon_2017.svg.png" width="15%">
</div>

这篇博文介绍了Blogger添加主页底部的分页导航组件，替换之前的"更多博文"按钮，以方便浏览阅读。</br>
<!-- more -->

<meting-js
	server="netease"
	type="song"
	id="407902">
</meting-js>

**TOC**

<!-- TOC -->

- [1. 关于Blogger自动分页(Auto Pagination)](#1-关于blogger自动分页auto-pagination)
- [2. 更换分页导航组件](#2-更换分页导航组件)
    - [2.1 添加css](#21-添加css)
    - [2.2 添加script](#22-添加script)
    - [2.3 参数配置](#23-参数配置)
- [参考(References)](#参考references)

<!-- /TOC -->

<a id="markdown-1-关于blogger自动分页auto-pagination" name="1-关于blogger自动分页auto-pagination"></a>
## 1. 关于Blogger自动分页(Auto Pagination)

******

Blogger的官方自动分页机制(Auto Pagination)是一个历史遗留问题，据官方博客的解释是为了加速博客的浏览以及降低延迟，具体可以参阅这份官方博文：[「Auto Pagination on Blogger」](https://blogger.googleblog.com/2010/02/auto-pagination-on-blogger.html?m=1)

> Latency is a word you hear a lot at Google. We are always looking for ways to make our products faster, because we have consistently found that faster page loads mean more satisfied users. This post is the first of an occasional series that will discuss ways in which we’re working to make blogs load faster for all users. --Vardhman Jain, Software Engineer, Mountain View

因此，Blogger的自动分页机制导致底部的分页导航组件只有一个简单"更多博文"按钮。

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/heirenwenhao.png" width="50%">
</div>

当你们博客主页的博文数超过页面展示上限数时，底部会出现以下分页导航按钮：

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/autopage1.png" width="100%">
</div>

虽然谷歌Blogger的工程师吹说为了加速浏览体验和降低延迟，但这个机制从2010年提出使用后，截至2019年已经被喷了9年了，那么截至现在就是被喷10年了...

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/autopage2.png" width="100%">
</div>

<a id="markdown-2-更换分页导航组件" name="2-更换分页导航组件"></a>
## 2. 更换分页导航组件

******

采用这篇博文作者提供的分页导航组件：[「How To Add Numbered Page Navigation Widget For Blogger」](https://helplogger.blogspot.com/2014/04/how-to-add-numbered-page-navigation-widget-for-blogger.html)

<a id="markdown-21-添加css" name="21-添加css"></a>
### 2.1 添加css

在范本XML中搜索`]]></b:skin>`，并且在该标签前添加css样式，具体的css样式作者提供了7种，可按个人需要选择：[>>>css样式传送门>>>](https://helplogger.blogspot.com/2014/04/how-to-add-numbered-page-navigation-widget-for-blogger.html)

例如灰色标签蓝色页码的样式：

```css
#blog-pager{clear:both;margin:30px auto;text-align:center; padding: 7px;}
.blog-pager {background: none;}
.displaypageNum a,.showpage a,.pagecurrent{font-size: 14px;padding: 5px 12px;margin-right:5px; color: #666; background-color:#eee;}
.displaypageNum a:hover,.showpage a:hover, .pagecurrent{background:#359BED;text-decoration:none;color: #fff;}
#blog-pager .pagecurrent{font-weight:bold;color: #fff;background:#359BED;}
 .showpageOf{display:none!important}
#blog-pager .pages{border:none;}
```

效果：

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/numberedpage1.png" width="100%">
</div>

另外，如果需要隐藏"First"和"Last"按钮，在上面代码的最后加上：

```css
.firstpage, .lastpage {display: none;}
```

<a id="markdown-22-添加script" name="22-添加script"></a>
### 2.2 添加script

在范本XML中搜索`</body>`，在该标签前添加以下脚本：

```xml
<b:if cond='data:blog.pageType != &quot;item&quot;'>
<b:if cond='data:blog.pageType != &quot;static_page&quot;'>
<script type='text/javascript'>
  /*<![CDATA[*/
    var perPage=3;
    var numPages=3;
    var firstText ='First';
    var lastText ='Last';
    var prevText ='« Previous';
    var nextText ='Next »';
    var urlactivepage=location.href;
    var home_page="/";

if(typeof firstText=="undefined")firstText="First";if(typeof lastText=="undefined")lastText="Last";var noPage;var currentPage;var currentPageNo;var postLabel;pagecurrentg();function looppagecurrentg(pageInfo){var html='';pageNumber=parseInt(numPages / 2);if(pageNumber==numPages-pageNumber){numPages=pageNumber*2+1}
pageStart=currentPageNo-pageNumber;if(pageStart<1)pageStart=1;lastPageNo=parseInt(pageInfo / perPage)+1;if(lastPageNo-1==pageInfo / perPage)lastPageNo=lastPageNo-1;pageEnd=pageStart+numPages-1;if(pageEnd>lastPageNo)pageEnd=lastPageNo;html+="<span class='showpageOf'>Page "+currentPageNo+' of '+lastPageNo+"</span>";var prevNumber=parseInt(currentPageNo)-1;if(currentPageNo>1){if(currentPage=="page"){html+='<span class="showpage firstpage"><a href="'+home_page+'">'+firstText+'</a></span>'}else{html+='<span class="displaypageNum firstpage"><a href="/search/label/'+postLabel+'?&max-results='+perPage+'">'+firstText+'</a></span>'}}
if(currentPageNo>2){if(currentPageNo==3){if(currentPage=="page"){html+='<span class="showpage"><a href="'+home_page+'">'+prevText+'</a></span>'}else{html+='<span class="displaypageNum"><a href="/search/label/'+postLabel+'?&max-results='+perPage+'">'+prevText+'</a></span>'}}else{if(currentPage=="page"){html+='<span class="displaypageNum"><a href="#" onclick="redirectpage('+prevNumber+');return false">'+prevText+'</a></span>'}else{html+='<span class="displaypageNum"><a href="#" onclick="redirectlabel('+prevNumber+');return false">'+prevText+'</a></span>'}}}
if(pageStart>1){if(currentPage=="page"){html+='<span class="displaypageNum"><a href="'+home_page+'">1</a></span>'}else{html+='<span class="displaypageNum"><a href="/search/label/'+postLabel+'?&max-results='+perPage+'">1</a></span>'}}
if(pageStart>2){html+=' ... '}
for(var jj=pageStart;jj<=pageEnd;jj++){if(currentPageNo==jj){html+='<span class="pagecurrent">'+jj+'</span>'}else if(jj==1){if(currentPage=="page"){html+='<span class="displaypageNum"><a href="'+home_page+'">1</a></span>'}else{html+='<span class="displaypageNum"><a href="/search/label/'+postLabel+'?&max-results='+perPage+'">1</a></span>'}}else{if(currentPage=="page"){html+='<span class="displaypageNum"><a href="#" onclick="redirectpage('+jj+');return false">'+jj+'</a></span>'}else{html+='<span class="displaypageNum"><a href="#" onclick="redirectlabel('+jj+');return false">'+jj+'</a></span>'}}}
if(pageEnd<lastPageNo-1){html+='...'}
if(pageEnd<lastPageNo){if(currentPage=="page"){html+='<span class="displaypageNum"><a href="#" onclick="redirectpage('+lastPageNo+');return false">'+lastPageNo+'</a></span>'}else{html+='<span class="displaypageNum"><a href="#" onclick="redirectlabel('+lastPageNo+');return false">'+lastPageNo+'</a></span>'}}
var nextnumber=parseInt(currentPageNo)+1;if(currentPageNo<(lastPageNo-1)){if(currentPage=="page"){html+='<span class="displaypageNum"><a href="#" onclick="redirectpage('+nextnumber+');return false">'+nextText+'</a></span>'}else{html+='<span class="displaypageNum"><a href="#" onclick="redirectlabel('+nextnumber+');return false">'+nextText+'</a></span>'}}
if(currentPageNo<lastPageNo){if(currentPage=="page"){html+='<span class="displaypageNum lastpage"><a href="#" onclick="redirectpage('+lastPageNo+');return false">'+lastText+'</a></span>'}else{html+='<span class="displaypageNum lastpage"><a href="#" onclick="redirectlabel('+lastPageNo+');return false">'+lastText+'</a></span>'}}
var pageArea=document.getElementsByName("pageArea");var blogPager=document.getElementById("blog-pager");for(var p=0;p<pageArea.length;p++){pageArea[p].innerHTML=html}
if(pageArea&&pageArea.length>0){html=''}
if(blogPager){blogPager.innerHTML=html}}
function totalcountdata(root){var feed=root.feed;var totaldata=parseInt(feed.openSearch$totalResults.$t,10);looppagecurrentg(totaldata)}
function pagecurrentg(){var thisUrl=urlactivepage;if(thisUrl.indexOf("/search/label/")!=-1){if(thisUrl.indexOf("?updated-max")!=-1){postLabel=thisUrl.substring(thisUrl.indexOf("/search/label/")+14,thisUrl.indexOf("?updated-max"))}else{postLabel=thisUrl.substring(thisUrl.indexOf("/search/label/")+14,thisUrl.indexOf("?&max"))}}
if(thisUrl.indexOf("?q=")==-1&&thisUrl.indexOf(".html")==-1){if(thisUrl.indexOf("/search/label/")==-1){currentPage="page";if(urlactivepage.indexOf("#PageNo=")!=-1){currentPageNo=urlactivepage.substring(urlactivepage.indexOf("#PageNo=")+8,urlactivepage.length)}else{currentPageNo=1}
document.write("<script src=\""+home_page+"feeds/posts/summary?max-results=1&alt=json-in-script&callback=totalcountdata\"><\/script>")}else{currentPage="label";if(thisUrl.indexOf("&max-results=")==-1){perPage=20}
if(urlactivepage.indexOf("#PageNo=")!=-1){currentPageNo=urlactivepage.substring(urlactivepage.indexOf("#PageNo=")+8,urlactivepage.length)}else{currentPageNo=1}
document.write('<script src="'+home_page+'feeds/posts/summary/-/'+postLabel+'?alt=json-in-script&callback=totalcountdata&max-results=1" ><\/script>')}}}
function redirectpage(numberpage){jsonstart=(numberpage-1)*perPage;noPage=numberpage;var nameBody=document.getElementsByTagName('head')[0];var newInclude=document.createElement('script');newInclude.type='text/javascript';newInclude.setAttribute("src",home_page+"feeds/posts/summary?start-index="+jsonstart+"&max-results=1&alt=json-in-script&callback=finddatepost");nameBody.appendChild(newInclude)}
function redirectlabel(numberpage){jsonstart=(numberpage-1)*perPage;noPage=numberpage;var nameBody=document.getElementsByTagName('head')[0];var newInclude=document.createElement('script');newInclude.type='text/javascript';newInclude.setAttribute("src",home_page+"feeds/posts/summary/-/"+postLabel+"?start-index="+jsonstart+"&max-results=1&alt=json-in-script&callback=finddatepost");nameBody.appendChild(newInclude)}
function finddatepost(root){post=root.feed.entry[0];var timestamp1=post.published.$t.substring(0,19)+post.published.$t.substring(23,29);var timestamp=encodeURIComponent(timestamp1);if(currentPage=="page"){var pAddress="/search?updated-max="+timestamp+"&max-results="+perPage+"#PageNo="+noPage}else{var pAddress="/search/label/"+postLabel+"?updated-max="+timestamp+"&max-results="+perPage+"#PageNo="+noPage}
location.href=pAddress}

  /*]]>*/
</script>
</b:if>
</b:if>
```

<a id="markdown-23-参数配置" name="23-参数配置"></a>
### 2.3 参数配置

以下是该分页导航组件可配置的参数以及意义：

```xml
perPage: 5, //单页博文数目的上限
numPages: 5, //分页导航组件显示的页数
var firstText ='First'; //首页按钮显示名
var lastText ='Last'; //尾页按钮显示名
var prevText ='« Previous'; //上一页按钮显示名
var nextText ='Next »'; //下一页按钮显示名
```

注意，关于参数项`perPage`的设置，需要与Blogger后台设置的上限数一致：

1. 博文"最多显示"设置： </br>
   在Blogger后台选择设置->博文、评论和分享->博文中，设置"最多显示"与`perPage`一致：

   <div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/numberedpage2.png" width="100%">
</div>
   
2. 博文小工具"主页上的博文数"设置： </br>
   在Blogger后台选择布局->页面主体->博文->主页选项中，设置"主页上的博文数"与`perPage`一致：

   <div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/numberedpage3.png" width="100%">
</div>

最终的效果类似下图：

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/numberedpage4.png" width="100%">
</div>

可以看出替换后的博客页面更便于浏览，这本是正常网页具备的基础功能，但是由于Auto Pagination的反人类机制导致博文数量较多时翻阅很不方便。

另外，分页导航组件的css和js文件可以打包上传对象存储空间配合CDN实现加速加载。

<a id="markdown-参考references" name="参考references"></a>
## 参考(References)

******

* [Auto Pagination on Blogger](https://blogger.googleblog.com/2010/02/auto-pagination-on-blogger.html?m=1) </br>
* [How To Add Numbered Page Navigation Widget For Blogger](https://helplogger.blogspot.com/2014/04/how-to-add-numbered-page-navigation-widget-for-blogger.html) </br>

<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>