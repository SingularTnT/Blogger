---
title: ''
---

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/valine.png" width="40%">
</div>

这篇博文介绍了Blogger更换Valine评论系统时出现评论组件加载失败，状态码为404，并且LeanCloud验证401 Unauthorized的处理方法。</br>
<!-- more -->

<meting-js
	server="netease"
	type="song"
	id="443919298">
</meting-js>

**TOC**

<!-- TOC -->

- [1. Blogger更换Valine评论](#1-blogger更换valine评论)
- [2. Valine验证出现 401 Unauthorized](#2-valine验证出现-401-unauthorized)
    - [2.1 错误详情](#21-错误详情)
    - [2.2 解决方式](#22-解决方式)
- [3. 使用Valine Admin管理评论](#3-使用valine-admin管理评论)
- [参考(References)](#参考references)

<!-- /TOC -->

<a id="markdown-1-blogger更换valine评论" name="1-blogger更换valine评论"></a>
## 1. Blogger更换Valine评论

******

[Valine](https://valine.js.org/)是一款基于LeanCloud的快速、简洁且高效的无后端评论系统，理论上支持但不限于静态博客，目前已有Hexo、Jekyll、Typecho、Hugo、Ghost 等博客程序在使用Valine。

魔改版的Valine可以移步至：[Valine: 独立博客评论系统](https://deserts.io/diy-a-comment-system/)

Blogger安装Valine评论组件可以参考：[为 Blogger 安装 Valine 评论系统](https://www.axutongxue.com/2019/05/blogger-valine.html)

主要步骤为： </br>
1. 在`</head>`标签前插入：
   
   ```xml
   <!--Leancloud 操作库:-->
    <script src="//cdn1.lncld.net/static/js/3.0.4/av-min.js"></script>
    <!--Valine 的核心代码库-->
    <script src="你托管的Valine路径./dist/Valine.min.js"></script>
   ```

2. 在`</body>`标签前插入：
   
   ```xml
   <script src="https://cdnjs.loli.net/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
   <script>
    window.onload = function(){
        new Valine({
            // AV 对象来自上面引入av-min.js(老司机们不要开车➳♡゛扎心了老铁)
            av: AV, 
            el: '.comment', // 
            app_id: 'Your APP ID', // 这里填写上面得到的APP ID
            app_key: 'Your APP KEY', // 这里填写上面得到的APP KEY
            placeholder: 'ヾﾉ≧∀≦)o来啊，快活啊!' // [v1.0.7 new]留言框占位提示文字
        });
    }
    </script>
   ```

3. 将范本XML中`<b:includable id='comments' var='post'>...</b:includable>`替换为：
   
   ```xml
   <b:includable id='comments' var='post'>
   <div class='comment'/>
   </b:includable>
   ```

<a id="markdown-2-valine验证出现-401-unauthorized" name="2-valine验证出现-401-unauthorized"></a>
## 2. Valine验证出现 401 Unauthorized

******

<a id="markdown-21-错误详情" name="21-错误详情"></a>
### 2.1 错误详情

完成以上步骤并且填好正确的"app_id"和"app_key"后，点击"保存主题背景"刷新页面，可以发现Valine组件已经成功嵌入，但是发现评论组件一直在loading但是无法加载出来：

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/Valineproblem.png" width="100%">
</div>

打开浏览器开发者工具，可以看到组件加载失败：

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/Valineproblem1.png" width="100%">
</div>

此时状态码为404，双击该请求得到LeanCloud错误码详情：

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/Valineproblem2.png" width="60%">
</div>

获得的错误码为`401`，根据[LeanCloud错误码详解](https://leancloud.cn/docs/error_code.html)，表明错误信息是：

· 信息 - Unauthorized. </br>
· 含义 - 未经授权的访问，没有提供 App id，或者 App id 和 App key 校验失败，请检查配置。

<a id="markdown-22-解决方式" name="22-解决方式"></a>
### 2.2 解决方式

LeanCloud提供的错误码详解并没有实际的参考意义，然后找到`@kveln`的教程发现需要在LeanCloud后台的储存->结构化数据中，创建一个"Comment"的class即可：

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/Valineproblem3.png" width="100%">
</div>

刷新博客页面，可以发现评论组件已经成功加载了：

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/Valineproblem4.png" width="100%">
</div>

由于使用的是国际版的LeanCloud，可能是这个原因导致的。

<a id="markdown-3-使用valine-admin管理评论" name="3-使用valine-admin管理评论"></a>
## 3. 使用Valine Admin管理评论

Valine Admin 是 Valine 评论系统的扩展和增强，主要实现评论邮件通知、评论管理、垃圾评论过滤等功能。支持完全自定义的邮件通知模板，基于Akismet API实现准确的垃圾评论过滤。

安装配置：[Valine Admin 配置手册](https://deserts.io/valine-admin-document/)

<a id="markdown-参考references" name="参考references"></a>
## 参考(References)

******

* [Valine -- 一款极简的评论系统](https://ioliu.cn/2017/add-valine-comments-to-your-blog/)
* [为你的Gridea博客加上Valine评论系统](https://kveln.cn/post/qE678A4ce/) </br>
* [为 Blogger 安装 Valine 评论系统](https://www.axutongxue.com/2019/05/blogger-valine.html)
* [Valine: 独立博客评论系统](https://deserts.io/diy-a-comment-system/)

<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>