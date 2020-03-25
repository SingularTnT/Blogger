---
title: ''
---

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/blogger-1200x630.png" width="100%">
</div>

这篇博文的主要内容是通过Blogger搭建国内可访问的个人博客，包括前提条件、解析设置、主题背景的选择与范本的修改方式、主题背景的几处关键修改以及更换评论系统，从而实现最基本的功能和较为流畅的访问体验。</br>
<!-- more -->

**TOC**
<!-- TOC -->

- [1. 前提条件](#1-前提条件)
    - [1.1. 科学上网](#11-科学上网)
    - [1.2. 一个域名](#12-一个域名)
    - [1.3. 图床](#13-图床)
    - [1.4. 对象存储空间](#14-对象存储空间)
- [2. Blogger解析设置](#2-blogger解析设置)
    - [2.1. 注册Blogger](#21-注册blogger)
    - [2.2. 国内可访问域名解析设置](#22-国内可访问域名解析设置)
- [3. 主题背景的选择与范本的修改方式](#3-主题背景的选择与范本的修改方式)
    - [3.1. 主题背景选择](#31-主题背景选择)
    - [3.2. 修改主题背景XML文件](#32-修改主题背景xml文件)
- [4. 主题背景的几处关键修改](#4-主题背景的几处关键修改)
    - [4.1. 修改个人头像和背景图片](#41-修改个人头像和背景图片)
    - [4.2. 修改博客网站的favicon和字体](#42-修改博客网站的favicon和字体)
    - [4.3. 屏蔽Blogger css、js文件自动加载项](#43-屏蔽blogger-cssjs文件自动加载项)
    - [4.4. 修改选项控件和搜索控件的js文件](#44-修改选项控件和搜索控件的js文件)
    - [4.5. 解决缩略图加载失败问题](#45-解决缩略图加载失败问题)
    - [4.6. 发布博文加载过慢问题](#46-发布博文加载过慢问题)
- [5. 更换评论系统](#5-更换评论系统)
- [6. 结语](#6-结语)
- [参考(References)](#参考references)

<!-- /TOC -->

虽然关于Blogger搭建国内可访问的博文很多，但还是决定自己记录一下，也当作自己博客的开头，“废话篇”请移步我的上一篇博文 > [「Hello Blogger」](https://www.weipingliu.com/2020/03/hello-blogger-blogger.html) </br>
P.S. 由于我自己的博客已经搭建完成，为了写这篇博文我注册了个新的Blogger账号和一个新的免费域名(:chicken:.cf)...:ghost: </br>

<a id="markdown-1-前提条件" name="1-前提条件"></a>
## 1. 前提条件

******

<a id="markdown-11-科学上网" name="11-科学上网"></a>
### 1.1. 科学上网

首先请确保自己可以访问谷歌的Blogger网站。 </br>
:link:测试：[>>>传送门>>>](https://www.blogger.com/)

<a id="markdown-12-一个域名" name="12-一个域名"></a>
### 1.2. 一个域名

* 域名购买渠道：</br>
   付费域名：[阿里云](https://www.aliyun.com/)、[腾讯云](https://cloud.tencent.com/)、[GoDaddy](https://sg.godaddy.com/)等 </br>
   免费域名：[Freenom](https://www.freenom.com/)(主要包括 .tk, .ml, .ga, .cf和.gq)

   *个人建议：长期使用的话尽量买 .com和 .cn的域名*

* 域名的Nameservers：</br>
   如果你在不同渠道购买购买了多个域名，可以将在它们的Nameservers转移到[Cloudflare](https://www.cloudflare.com/)中以方便管理，这方面的详细教程有很多，具体可以参考：[「将您的域名服务器更改为 Cloudflare」](https://support.cloudflare.com/hc/zh-cn/articles/205195708-%E5%B0%86%E6%82%A8%E7%9A%84%E5%9F%9F%E5%90%8D%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%9B%B4%E6%94%B9%E4%B8%BA-Cloudflare)，我这里介绍一下关键的步骤。 </br>
   以[GoDaddy](https://sg.godaddy.com/)为例，在My Account->Domain Manager->DNS Management中将"Nameservers"这一项修改为Cloudflare的名称服务器：

   ```
   opal.ns.cloudflare.com
   rohin.ns.cloudflare.com
   ```

   <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/godaddy1.png" width="100%">
    </div>

   完成以上操作和Cloudflare验证状态有效后，就可以在Cloudflare的"DNS"选项中配置域名解析了：

   <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/cloudflare1.png" width="100%">
    </div>

<a id="markdown-13-图床" name="13-图床"></a>
### 1.3. 图床

图床看个人的选择，我自己使用的比较简单且易实现的是Github + PicGo+ jsDelivr CDN组合，Github的仓库用于存素材，PicGo负责上传至Github同时配置好指定域名，而jsDelivr负责缓存加速，这方面有很多详细的搭建教程，移步[「dogedoge：关键词PicGo+Github+jsDelivr」](https://www.dogedoge.com/results?q=PicGo%2BGithub%2BjsDelivr)。

配置好后获得图片外链仅需两步，第一步上传图片：

<div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/picgo1.png" width="100%">
    </div>

第二步，复制图片外链：

<div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/picgo2.png" width="100%">
    </div>

整个使用过程非常的流畅和方便，虽然目前PicGo有一些图片格式(如.ico)不支持，而且会有一些小bug(重启软件大法好)，但是整体上还是非常方便的。

这种方式的一个缺陷就是当你们CDN挂了后处理之前博客的图片就比较麻烦了，所以有这方面顾虑的可以考虑自建图床。

<a id="markdown-14-对象存储空间" name="14-对象存储空间"></a>
### 1.4. 对象存储空间

对象存储空间服务提供商有很多可以选择的，V站有个相关帖移步[「求推荐对象存储服务」](https://www.v2ex.com/t/607505)，以下列举一些比较常见的：

* [阿里云](https://www.aliyun.com/)
* [腾讯云](https://cloud.tencent.com/)
* [AWS](https://aws.amazon.com/)
* [又拍云](https://www.upyun.com/)
* [七牛云](https://www.qiniu.com/)

由于我的域名是腾讯云上买的，因此对象存储也选择了腾讯云(前六个月免费)，在腾讯云中选择我的->云产品->对象存储->存储桶列表中点击"创建存储桶"，即可在里面上传对象文件。

需要注意的是，在对象的详情->对象权限->公共权限中，需要更改默认权限为"公有读私有写"：

<div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/txyunduixiang1.png" width="100%">
    </div>

<a id="markdown-2-blogger解析设置" name="2-blogger解析设置"></a>
## 2. Blogger解析设置

******

<a id="markdown-21-注册blogger" name="21-注册blogger"></a>
### 2.1. 注册Blogger

在[Blogger官网](https://www.blogger.com/)注册一个账号，需要注意的是Blogger是一项谷歌的服务，仅限Gmail账号登录。

<a id="markdown-22-国内可访问域名解析设置" name="22-国内可访问域名解析设置"></a>
### 2.2. 国内可访问域名解析设置

由于国内无法直接访问Blogger，见Wiki的[「404网站清单」](https://zh.wikipedia.org/wiki/Category:%E8%A2%AB%E9%98%B2%E7%81%AB%E9%95%BF%E5%9F%8E%E5%B0%81%E9%94%81%E7%9A%84%E7%BD%91%E7%AB%99)，这一步的主要目的是通过第三方网域设置实现国内可访问。

1. Blogger第三方网域设置 </br>
   打开Blogger的设置->基本->发布，选择"修改"，可以看到如下的配置选项：

    <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/BloggerCNAME.png" width="100%">
    </div>

   根据设置提示需要在你的域名系统(DNS)解析中输入`ghs.google.com`和`xxx.dv.googlehosted.com`两个CNAME记录。而其中的`ghs.google.com`已经被GFW所屏蔽无法直接访问，`ghs.google.com`不提供实质性服务，而只是选择访问者访问Google全球边缘网络中最快的服务器。因此我们可以从国内可接入的Google全球边缘网络服务器中选取合适的固定IP进行访问，并且设定为A记录解析。

2. 寻找国内可访问的IP地址 </br>
   通过一些网络测试工具如[站长工具](http://ping.chinaz.com/)，Ping服务器`ghs.google.com`：

   <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/zhanzhangping2.png" width="100%">
    </div>
   
   从获取的监测结果中选取"响应时间"不超时且较短的合适大陆地区IP，类似下图所示，记作「国内可访问IP: `a.b.c.d`」：

   <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/zhanzhangpingtest.png" width="100%">
    </div>

   结合Blogger"第三方网域设置"中的另外一个CNAME记录，我们得到了两个解析：

   ```
   A解析：a.b.c.d(例如上图红框的"172.217.160.83")
   CNAME解析：xxx.dv.googlehosted.com
   ```
   
3. DNS解析 </br>
   打开你拥有的域名的Nameservers后台，这里以腾讯云为例，选择我的->云产品->DNS解析DNSPod->解析：

   <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/txyunyuming1.png" width="100%">
    </div>

   在记录管理中选择添加记录，添加两条A记录和一条CNAME记录，将上一个步骤的获得的国内可访问IP地址作为A记录解析，以及Blogger第三方网域设置中第二条的CNAME作为CNAME记录解析：

   <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/txyunjiexi1.png" width="100%">
    </div>

   等待一段生效时间后，关闭代理测试一下是否可以直接访问。

4. 启用HTTPS </br>
   根据这份官方博文[「HTTPS support coming to Blogspot」](https://blogger.googleblog.com/2015/09/https-support-coming-to-blogspot.html)，Blogger已于15年开始支持HTTPS。开启的方式非常简单，打开Blogger的设置->基本->HTTPS，修改"HTTPS 可用性"和"HTTPS 重定向"即可：

   <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/BloggerHTTPS.png" width="100%">
    </div>

<a id="markdown-3-主题背景的选择与范本的修改方式" name="3-主题背景的选择与范本的修改方式"></a>
## 3. 主题背景的选择与范本的修改方式

******

<a id="markdown-31-主题背景选择" name="31-主题背景选择"></a>
### 3.1. 主题背景选择

Blogger的主题背景主要分为官方的和非官方的模板

* 非官方范本： </br>
  对于非官方的模板我这里不作示例，可以参考"标签"为[「Blogger-Blogger 範本」](https://www.wfublog.com/search/label/%E9%9B%BB%E8%85%A6-%20Blogger-Blogger%20%E7%AF%84%E6%9C%AC?&max-results=5)的博文去自定义。

* 官方范本： </br>
  目前官方提供了"Contempo"、"Soho"、"Emporio"、"知名"等一系列模板：

  <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/officaltheme.png" width="100%">
    </div>

  根据[*@阿虚*](https://www.axutongxue.com/)和[*@JoeyLiu*](https://blog.iljw.me/)的教程建议，"Contempo"模板易于修改和优化，因此这里以"Contempo"主题背景为例进行说明。

<a id="markdown-32-修改主题背景xml文件" name="32-修改主题背景xml文件"></a>
### 3.2. 修改主题背景XML文件

修改主题背景的XML文件有两种方式，第一种是直接在线修改，第二种为通过"备份/还原"的方式上传和下载范本文件。

*建议：无论选择哪种方式，修改范本前记得备份。*

* 直接修改： </br>
  选择「主题背景」选项卡，点击"修改HTML"即可进入相应页面：

  <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/beifenhuanyuantheme1.png" width="100%">
    </div>

* 备份/还原： </br>
  通过"备份/还原"的方式，先选择「主题背景」选项卡，然后点击"备份/还原"即可下载和上传范本的XML文件：

  <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/beifenhuanyuantheme.png" width="100%">
    </div>

<a id="markdown-4-主题背景的几处关键修改" name="4-主题背景的几处关键修改"></a>
## 4. 主题背景的几处关键修改

******

上一节介绍了范本XML文件修改的两种方式，这部分以直接在线修改方式为例，通过修改主题背景设计器和范本XML文件达到所需效果。 </br>
P.S. 以下图片的外链为所用图床(我用的Github+PicGo+jsDelivr CDN)对应的图片链接，js文件的地址为所用对象存储(我用的腾讯云OSS)对应的对象地址。

<a id="markdown-41-修改个人头像和背景图片" name="41-修改个人头像和背景图片"></a>
### 4.1. 修改个人头像和背景图片

1. 设置头像和背景图片 </br>
   通常来说，在设置->用户设置->基本->用户个人资料中，点击"修改"，在「个人资料照片」处可以上传并保存头像：

   <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/modifyheadpic.png" width="100%">
    </div>
   
   在主题背景->自定义->背景->背景图片中，点击下拉箭头，可以选择上传背景图片或者贡献者提供的背景图片：

   <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/modifybgpic.png" width="100%">
    </div>
   
   但是当我们不通过代理直接访问网站的时候，会出现头像和背景图片无法显示的情况，这是因为你通过Blogger页面上传的图片信息都存在谷歌的服务器上，因此无法直接加载出来：

   <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/headpicaccess.png" width="100%">
    </div>
   
2. 修改范本中头像和背景图对应的代码 </br>
   **头像代码修改：** </br>
   在范本XML中搜索`class='profile-img'`，大约在3909行处可以找到以下代码：

   ```xml
   <img class='profile-img' expr:alt='data:messages.myPhoto' expr:height='data:authorPhoto.height' expr:src='data:authorPhoto.image' expr:width='data:authorPhoto.width'/>
   ```

   将`expr:src='dat:authorPhoto.image`修改为`src='你的头像外链'`即可。

   **背景图片代码修改：** </br>
   在范本XML中搜索`Variable name="body.background"`，大约在46行处可以找到以下代码：

   ```xml
   <Variable name="body.background" description="Background"
      color="$(body.background.color)"
      type="background"
      default="$(color) none repeat scroll top left"  value="$(color) url(https://themes.googleusercontent.com/image?id=L1lcAxxz0CLgsDzixEprHJ2F38TyEjCyE3RSAjynQDks0lT1BDc1OxXKaTEdLc89HPvdB11X9FDw) no-repeat scroll top center /* Credit: Michael Elkan (http://www.offset.com/photos/394244) */;"/>
   ```

   将`url(xxx)`修改为`url(你的背景图片外链)`即可。

   完成以上修改后，点击保存主题背景，我们再次关闭代理同时清除浏览器cache(Chrome快捷键：Ctrl+Shift+Del)，访问博客的主页时可以看到头像和背景图片均可以正常显示了：

   <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/headpicaccess1.png" width="100%">
    </div>

<a id="markdown-42-修改博客网站的favicon和字体" name="42-修改博客网站的favicon和字体"></a>
### 4.2. 修改博客网站的favicon和字体

1. 修改favicon </br>
   注意，修改网站favicon的前提条件是使用旧版的Blogger，因为新版的Blogger的布局中是没有修改网页图标的组件。
   
   旧版Blogger布局： </br>
   
   <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggeroldlayout.png" width="100%">
    </div>

   新版Blogger布局： </br>

   <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggernewlayout.png" width="100%">
    </div>

   点击旧版Blogger布局中的网页图标"修改"即可替换为自定义的favicon：
   
   <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/favcioneditafter.png" width="50%">
    </div>

2. 修改字体 </br>
   如果遇到在移动端出现标题不显示的情况，可以尝试通过Blogger主题背景设计器中修改字体。在Blogger后台打开主题背景->自定义->高级->博文，将对应的字体统一成"Arial"，然后点击"应用于博客"：

   <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggerfontmodify.png" width="100%">
    </div>

<a id="markdown-43-屏蔽blogger-cssjs文件自动加载项" name="43-屏蔽blogger-cssjs文件自动加载项"></a>
### 4.3. 屏蔽Blogger css、js文件自动加载项

幸运的是"Contempo"的范本XML文件中包含的自动加载项较少，并且默认的设定代码中已包含`b:css='false'`：

```xml
<html b:css='false' b:defaultwidgetversion='2' b:layoutsVersion='3' b:responsive='true' b:templateUrl='indie.xml' b:templateVersion='1.3.0'
```

因此我们只需将范本XML文件中的标签，简单按照如下方式进行替换：</br>
* 将`<head>`标签替换为：
  
  ```xml
  &lt;!--<head>--&gt;&lt;head&gt;
  ```

* 将`</head>`标签替换为：
  
  ```xml
  &lt;/head&gt;&lt;!--</head>--&gt;
  ```

* 将`</body>`标签替换为：
  
  ```xml
  &lt;!--</body>--&gt;&lt;/body&gt;
  ```

修改后点击"保存主题背景"。

<a id="markdown-44-修改选项控件和搜索控件的js文件" name="44-修改选项控件和搜索控件的js文件"></a>
### 4.4. 修改选项控件和搜索控件的js文件

在关闭代理的情况下，会发现选项控件和搜索控件点击无反应：

<div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggersearch.png" width="100%">
    </div>

怎么肥四，我们打开浏览器的开发者工具(Chrome快捷键: F12 or Ctrl+Shift+I)，清除cache后选择「Network」选项卡，然后刷新页面(Chrome快捷键: Ctrl+R)可以看到如下结果：

<div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggersearchjs1.png" width="100%">
    </div>

单击这个红色的`xxx-indie_compiled.js`，在「Headers」选项卡页面可以看到网页请求的URL：

<div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggersearchjs2.png" width="100%">
    </div>

我们复制这个URL在浏览器打开，然后右键保存到本地后上传到自己的对象存储空间中，记得设置对象的公共访问权限为"公有读私有写"！然后点击复制这个对象的地址：

<div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggersearchjs3.png" width="100%">
    </div>

回到范本XML文件中，找到以下这行代码：

```xml
<b:template-script async='true' name='indie' version='1.0.0'/>
```

删除或者注释掉该行代码，然后将上一步复制的对象地址填入如下代码中：

```xml
<script async='async' src='js对象地址(格式为：xxx-indie_compiled.js)'/>
```

将以上代码插入`<head>`标签后`</head>`标签前，如下所示：

<div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggersearchjs4.png" width="100%">
    </div>

点击"保存主题背景"后，关闭代理清空cache后测试选项控件和搜索控件是否有响应，这个时候打开浏览器的开发者工具应该可以看到js加载成功，控件点击有反应，URL指向了自己对象存储空间的对象地址以及状态码为`200 OK`：

<div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggersearchjs5.png" width="100%">
    </div>

<a id="markdown-45-解决缩略图加载失败问题" name="45-解决缩略图加载失败问题"></a>
### 4.5. 解决缩略图加载失败问题

当完成了上面的步骤，我们发布一篇博文到Blogger上，会发现当不开代理的情况下博文的缩略图无法显示：

<div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggerthumbnail.png" width="100%">
    </div>

根据[*@JoeyLiu*](https://blog.iljw.me/2019/07/blogger-thumbnail.html)提供的几种解决办法，我们选择嵌入JavaScript代码的方式。范本XML文件中的`snippet-thumbnail`和`post-thumbnail`是有关缩略图的部分，修改XML文件，将以下代码嵌入到`</body>`标签前：

```xml
<!--如果当前页是首页&#65292;搜索页&#65292;标签页&#65292;那么代码继续执行-->
  <b:if cond='data:blog.pageType in {&quot;index&quot;,&quot;searchQuery&quot;,&quot;searchLabel&quot;,&quot;archive&quot;,&quot;item&quot;}'>
      <script defer='defer'>
          //<![CDATA[
          var postThumbnails = document.getElementsByClassName("post-thumbnail");
          var postContents = document.getElementsByClassName("post-text");
          for (var i=0;i<postContents.length;i++)
          {
              var postContent = postContents[i].innerText;
              var imgReg = /<img.*?(?:>|\/>)/gi;
              var srcReg = /src=[\'\"]?([^\'\"]*)[\'\"]?/i;
              var imgTags = postContent.match(imgReg);
              imgSrcs = imgTags[0].match(srcReg);
              imgSrc = imgSrcs[1];
              postThumbnails[i].setAttribute('src', imgSrc);
          }
          //]]>
      </script>
  </b:if>
```

如下所示：

<div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggerthumbnail1.png" width="100%">
    </div>

接下来找到原有的缩略图代码进行修改，搜索`<b:if cond='data:post.featuredImage'>`，可以找到两处如下形式的代码：

```xml
<b:if cond='data:post.featuredImage'>
<div class='snippet-thumbnail'>
   <b:include data='{                                     image: data:post.featuredImage,                                     imageSizes: [32, 64, 128, 256],                                     imageRatio: &quot;1:1&quot;,                                     sourceSizes: &quot;(max-width: 800px) 20vw, 128px&quot;                                  }' name='responsiveImage'/>
</div>
</b:if>
```

删除或者注释两处以上代码，并且替换为如下代码：

```xml
<b:if cond='data:post.featuredImage'>  <!--判断文章内是否有图片&#65292;有则代码继续执行-->
<div class='snippet-thumbnail'>  <!--创建一个 div 容器&#65292;缩略图放置在这里-->
      <img class='post-thumbnail' sizes='(max-width: 800px) 20vw, 128px' src='https://ae01.alicdn.com/kf/HTB1Gb7LUmzqK1RjSZFL5jcn2XXac.gif'/>  <!--预先放置一个加载图片&#65292;增强用户体验-->
      <textarea class='post-text' style='display:none;'><data:post.body.escaped/></textarea> <!--这里放置文章全文&#65292;图片从中提取&#65292;样式设置为不显示-->
</div>
</b:if>
```

点击"保存主题背景"后，关闭代理并刷新页面可以看到缩略图已经成功加载：

<div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggerthumbnail2.png" width="100%">
    </div>

<a id="markdown-46-发布博文加载过慢问题" name="46-发布博文加载过慢问题"></a>
### 4.6. 发布博文加载过慢问题

根据上一步的步骤我们成功的解决了缩略图的问题，但是当我们发布博文后，会发现在关闭代理的时候网页的访问速度很慢。打开浏览器的开发者工具，点击「Network」选项卡后刷新页面，可以发现一个"耗电大户"：

<div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggerlogoload1.png" width="100%">
    </div>

展开这个加载项，我们可以看到它的详细信息：

<div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggerlogoload2.png" width="100%">
    </div>

请求的URL为`https://lh3.googleusercontent.com/zFdxGE77vvD2w5xHy6jkVuElKv-U9_9qLkRYK8OnbDeJPtjSZ82UPq5w6hJ-SA=w35`，根据Blogger官方技术人员的描述，和`lh3.googleusercontent.com`相关的资源是属于谷歌产品服务中的，因此这个请求的地址会直接到谷歌的服务器，很显然会加载失败：

<div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggerlh3.png" width="100%">
    </div>

按道理我们的图片资源都是存在自己的图床中的，我们在浏览器中打开这个链接看一下请求的是什么资源：

<div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggerlogoload3.png" width="50%">
    </div>

这个圆形的Blogger icon我在Blogger的页面中暂时也没有发现在哪出现过。下面选择直接把它存到自己的图床以加速访问，在浏览器开发者工具中的单击这个资源，选择「Initiator」选项卡，可以在请求链中找到它的源头在`xxx-indie_compiled.js`文件中，这就是之前在"修改选项控件和搜索控件的js文件"这一部分所使用的js文件。

我们打开`xxx-indie_compiled.js`文件，搜素`https://lh3.googleusercontent.com`可以找到这个资源出现的位置：

```javascript
a.src="https://lh3.googleusercontent.com/zFdxGE77vvD2w5xHy6jkVuElKv-U9_9qLkRYK8OnbDeJPtjSZ82UPq5w6hJ-SA=w35";
```

将其修改为：

```javascript
a.src="该资源的外链";
或者直接删除
a.src="";
```

将修改后的`xxx-indie_compiled.js`重新上传到原来的对象存储空间中替换之前的对象，再在浏览器开发者工具中请求后发现该资源可以快速成功的加载或者直接不加载该资源，并且没有明显拖后腿的请求：

<div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggerlogoload5.png" width="100%">
    </div>

<a id="markdown-5-更换评论系统" name="5-更换评论系统"></a>
## 5. 更换评论系统

******

由于Blogger的评论系统需要谷歌服务和Gmail账户，因此无代理情况下无法加载评论系统：

<div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggercomment.png" width="100%">
    </div>

可以考虑更换的评论系统有： </br>
* [Gitalk](https://gitalk.github.io/)：基于Github Issue和Preact的评论系统，可以直接登录Github账户进行评论留言。 </br>
  具体移步：[「为 Blogger 安装 Gitalk 评论系统」](https://blog.iljw.me/2019/02/blogger-gitalk.html)
* [LiveRe](http://livere.com/)：可以通过QQ、微信、微博等国内社交账户登录，但是加载速度比较慢。 </br>
  具体移步：[「给Blogger添加来必力评论系统」](https://www.axutongxue.com/2018/10/blogger_13.html)
* [Valine](https://valine.js.org/)：基于Leancloud的无后端评论系统，加载速度很快还可以自定义表情，支持Markdown。 </br>
  具体移步：[「为 Blogger 安装 Valine 评论系统」](https://www.axutongxue.com/2019/05/blogger-valine.html)

<a id="markdown-6-结语" name="6-结语"></a>
## 6. 结语

******

至此，关于主题背景和相关组件的关键修改基本完成，国内可访问的基础功能也已实现，并且可以达到较快的访问速度。

但是这样处理后的Blogger还有两处无伤大雅的缺陷：

1. 个人资料无法访问 </br>

   点击我的简介区域发现无法访问此网页：

   <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggerpersonalfile.png" width="100%">
    </div>

2. 分享控件无效 </br>

   点击分享控件发现无响应：

   <div align=center>
    <img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/bloggershare.png" width="100%">
    </div>

后续还有很多可以自定义和优化的地方，如关于访问速度的优化，可以通过浏览器开发者工具进行调试，找到Load时间较长的请求进行分析，例如是js文件就存储到国内的对象存储空间，而对于css文件可以通过参考[「Blogger 新手入門（筆記）」](https://www.wfublog.com/2013/04/blogger-guide-note.html)后对一些文件进行打包再存储到对象存储空间中。

关于"Blogger"这个Tag，后续的博客我可能会更新一些关于Blogger样式的修改、写作方式和发布方式的推荐以及SEO等方面的内容:bird:。

Markdown写作方式的推荐：

1. (★★★★☆) VSCode </br>
   VSCode拥有丰富的插件，写好md直接导出html复制到Blogger上。
2. (★★★☆☆) Typora + Chrome StackEdit </br>
   Typora专注优雅写作，然后将源文件复制到Chrome的StackEdit插件直接Publish，非常流畅。
3. (★★☆☆☆) Blogger + Chrome Markdown Here </br>
   直接在Blogger后台在线写博文，无法实时预览，写好Markdown格式后通过Chrome的Markdown Here插件在线生成html。

这篇博文主要参考了[*@阿虚*](https://www.axutongxue.com/)、[*@JoeyLiu*](https://blog.iljw.me/)、[*@LawyerFu*](https://www.lawpai.com/)和[*@臧超*](http://www.geooll.com/)的教程，并且得到了"谷歌blogger交流群：125691905"的帮助。

<a id="markdown-参考references" name="参考references"></a>
## 参考(References)

******

* [Blogger搭建国内可正常访问博客（超详细教程）](https://www.axutongxue.com/2018/10/httpsws1.html) </br>

* [找到一个可以替代ghs.google.com的地址](https://sites.google.com/site/heartsoverview/systems/tips/resolved/ghs) </br>

* [Blogger 国内访问心得](https://blog.iljw.me/2016/09/blogger.html) </br>

* [CNAME record values](https://support.google.com/a/answer/112038?hl=en)

* [为博客启用 HTTPS](https://support.google.com/blogger/answer/6284029?hl=zh-Hans)

* [BLOGGER 終於支援 HTTPS﹍搞懂安全傳輸協定的重要性及影響](https://www.wfublog.com/2015/10/blogger-https-guide.html)


