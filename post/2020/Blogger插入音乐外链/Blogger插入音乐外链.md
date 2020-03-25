---
title: ''
---

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/MettingJS1.png" width="100%">
</div>

这篇博文介绍了一种Blogger插入音乐外链的方式，通过在Markdown中插入MetingJS插件和相关音乐外链信息导出生成HTML，从而达到在博客中插入音乐外链播放的效果。</br>
<!-- more -->

**TOC**

<!-- TOC -->

- [1. 国内音乐服务平台](#1-国内音乐服务平台)
- [2. 提取歌曲外链](#2-提取歌曲外链)
    - [2.1. 直接生成外链播放器](#21-直接生成外链播放器)
    - [2.2. 间接获取外链播放器](#22-间接获取外链播放器)
- [3. 插入歌曲外链](#3-插入歌曲外链)
    - [3.1 官方方式：](#31-官方方式)
    - [3.2 使用MetingJS插件插入外链(推荐)：](#32-使用metingjs插件插入外链推荐)
- [参考(References)](#参考references)

<!-- /TOC -->

**声明：以下内容仅用于学习和交流，请勿用于其他用途！** 

<a id="markdown-1-国内音乐服务平台" name="1-国内音乐服务平台"></a>
## 1. 国内音乐服务平台

******

国内音乐服务平台有很多，典型的有：

* [网易云音乐(netease)](https://music.163.com/)
* [QQ音乐(tencent)](https://y.qq.com/)
* [虾米音乐(xiami)](https://www.xiami.com/)
* [酷狗音乐(kugou)](https://www.kugou.com/)
* [千千音乐(baidu)](http://music.taihe.com/)

这里仅以网易云音乐示例。

<a id="markdown-2-提取歌曲外链" name="2-提取歌曲外链"></a>
## 2. 提取歌曲外链

******

<a id="markdown-21-直接生成外链播放器" name="21-直接生成外链播放器"></a>
### 2.1. 直接生成外链播放器

对于无版权问题的歌曲，可以直接在网易云音乐中选择"生成外链播放器"：

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/outchain1.png" width="100%">
</div>

网易云音乐提取的外链主要包括"iframe插件"和"flash插件"，前者基于HTML后者基于Flash，推荐使用前者：</br>

**iframe插件**：

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/outchainiframe.png" width="100%">
</div>

**flash插件**：

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/outchainflash.png" width="100%">
</div>

<a id="markdown-22-间接获取外链播放器" name="22-间接获取外链播放器"></a>
### 2.2. 间接获取外链播放器

对于存在版权问题的歌曲，可以通过修改`id`的方式获取外链播放器，如上一步在网易云音乐中获取的iframe插件外链代码为：

```xml
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=454180&auto=1&height=66"></iframe>
```

其中`id=xxx`可以直接修改为对应歌曲的网页链接`id`即可，算是间接获得了外链：

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/outchainid.png" width="100%">
</div>

<a id="markdown-3-插入歌曲外链" name="3-插入歌曲外链"></a>
## 3. 插入歌曲外链

******

<a id="markdown-31-官方方式" name="31-官方方式"></a>
### 3.1 官方方式：

直接在Markdown中插入以下代码即可：

**iframe插件**：

```xml
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=454180&auto=1&height=66"></iframe>
```

效果：

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=454180&auto=0&height=66"></iframe>

**flash插件**：

```xml
<embed src="//music.163.com/style/swf/widget.swf?sid=454180&type=2&auto=1&width=320&height=66" width="340" height="86"  allowNetworking="all"></embed>
```
效果：

<embed src="//music.163.com/style/swf/widget.swf?sid=454180&type=2&auto=0&width=320&height=66" width="340" height="86"  allowNetworking="all"></embed>

**缺点**： </br>
* 没有滚动歌词
* 有版权问题的歌曲只能显示无法播放

<a id="markdown-32-使用metingjs插件插入外链推荐" name="32-使用metingjs插件插入外链推荐"></a>
### 3.2 使用MetingJS插件插入外链(推荐)：

MetingJS是一个结合了APlayer和Meting的开源音乐播放外链插件，可选参数很多而且可以绕开版权问题，提供多平台支持和歌曲歌词滚动条。

提供多种播放形式： </br>
* song
* playlist
* album
* search
* artist

具体内容移步 > [MetingJS](https://github.com/metowolf/MetingJS)

使用步骤：
1. 在Markdown开头或者结尾处插入以下代码：
   
   ```xml
   <!-- require APlayer -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
    <script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
    <!-- require MetingJS -->
    <script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>

   ```

2. 在需要置放音乐外链播放器处插入类似以下代码：
   
   ```xml
   <meting-js
        server="netease"
        type="song"
        id="454180">
    </meting-js>
   ```

效果如下：

<meting-js
	server="netease"
	type="song"
	id="454180">
</meting-js>

可选参数列表：

|option               |default      |description|
|:--------------------|:------------:|:----------|
|id              |**require**   |song id / playlist id / album id / search keyword|
|server          |**require**   |music platform: `netease`, `tencent`, `kugou`, `xiami`, `baidu`|
|type            |**require**   |`song`, `playlist`, `album`, `search`, `artist`|
|auto            |options       |music link, support: `netease`, `tencent`, `xiami`|
|fixed           |`false`       |enable fixed mode|
|mini            |`false`       |enable mini mode|
|autoplay        |`false`       |audio autoplay|
|theme           |`#2980b9`     |main color|
|loop            |`all`         |player loop play, values: 'all', 'one', 'none'|
|order           |`list`        |player play order, values: 'list', 'random'|
|preload         |`auto`        |values: 'none', 'metadata', 'auto'|
|volume          |`0.7`         |default volume, notice that player will remember user setting, default volume will not work after user set volume themselves|
|mutex           |`true`        |prevent to play multiple player at the same time, pause other players when this player start play|
|lrc-type         |`0`           |lyric type|
|list-folded      |`false`       |indicate whether list should folded at first|
|list-max-height   |`340px`       |list max height|
|storage-name     |`metingjs`    |localStorage key that store player setting|

综合以上推荐使用MetingJS插件，可以提供更好的效果和更多可选的参数。

<a id="markdown-参考references" name="参考references"></a>
## 参考(References)

******

* [A powerful plugin connect APlayer and Meting](https://github.com/metowolf/MetingJS) </br>

<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>