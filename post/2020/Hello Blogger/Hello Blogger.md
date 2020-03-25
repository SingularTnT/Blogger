---
title: ''
---

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/Blogger_icon_2017.svg.png" width="15%">
</div>

折腾了几个搭建博客的方式，不是被墙了就是换电脑换系统要重新配环境，放弃了不想折腾了，选择拥抱Blogger。</br>
这篇博文主要是关于我搭建博客的想法，介绍一些试过及了解过的搭建博客的方式以及为什么选择Blogger。</br>
<!-- more -->

**TOC**
<!-- TOC -->

- [一. 关于搭建博客的想法](#一-关于搭建博客的想法)
- [二. 搭建博客的方式](#二-搭建博客的方式)
    - [1. 废话篇](#1-废话篇)
    - [2. 几种搭建博客的方式](#2-几种搭建博客的方式)
    - [3. 补充说明](#3-补充说明)
- [三. 为什么选择Blogger](#三-为什么选择blogger)
    - [1. Blogger介绍](#1-blogger介绍)
    - [2. Blogger国内使用问题](#2-blogger国内使用问题)
    - [3. 选Blogger的想法](#3-选blogger的想法)
- [参考(References)](#参考references)

<!-- /TOC -->

<a id="markdown-一-关于搭建博客的想法" name="一-关于搭建博客的想法"></a>
## 一. 关于搭建博客的想法

******

由于懒癌一直没有写日记记笔记的习惯，接触博客后也基本没有怎么写过博客。但是我的记忆力极差，经常学过的东西隔几天就忘了，所以我觉得我适合在某个非常细分的领域内走下去，然而现实是非常残酷的。为了不让很多走过的路再走一遍，我打算开始用博客记录一些技术内容和生活日志。

<a id="markdown-二-搭建博客的方式" name="二-搭建博客的方式"></a>
## 二. 搭建博客的方式

******

<a id="markdown-1-废话篇" name="1-废话篇"></a>
### 1. 废话篇

搭建博客的方式有很多种，主要分为静态博客和动态博客的区别，V2EX上有一个关于这方面选择的讨论贴可以参考一下 > [「静态博客生成器 OR 动态博客？」](https://www.v2ex.com/t/154179)

我个人其实兜兜转转了很多次，也用了很多方式，但是回头发现自己的大部分时间都拿来试各种博客框架以及改前端去了，反而没写几篇博客，有点买椟还珠的感觉。沉思后觉得还是背靠谷歌Blogger放弃各种花里胡哨的操作。

我的迁移路线：WordPress -> Hexo -> Hugo -> Blogger

<a id="markdown-2-几种搭建博客的方式" name="2-几种搭建博客的方式"></a>
### 2. 几种搭建博客的方式

但还是简单介绍一些使用过和了解过的搭建个人博客的方式：

1. **WordPress & LAMP**:
   
   > *WordPress是当前因特网上最流行的博客系统。  --Wikipedia*

   想必这个不用多说了吧，[WordPress](https://wordpress.com/)是目前最受欢迎的网站内容管理系统。我最早就是用的这种方式搭建动态博客，买了个VPS和域名，通过[LAMP](https://lamp.sh/)环境和WordPress在CentOS7上搭建的博客。但是后面服务器IP被墙了然后就考虑转移到静态博客阵营。

   优点：功能强大，插件丰富，而且有CMS </br>
   缺点：需要自备主机，国内需要备案还是挺麻烦的 </br>

2. **Hexo & Github Pages**:
   
   [Hexo](https://hexo.io/)可以说是目前国内非常流行的静态博客框架了，插件丰富也有很多的贡献者做的主题可选，基于Node.js对网页进行渲染再部署到[Github Pages](https://pages.github.com/)等平台进行托管。如果不用Github actions或者Gitlab的CI/CD，需要在本地环境进行HTML生成再部署到线上，重点是本地环境如果你装了很多插件换电脑或者换系统的时候会非常不方便，另外Hexo+Github Pages速度都很慢:turtle:，另外注意一点就是Github Pages把百度爬虫ban了，所以得后续考虑cdn之类的方式，这里不赘述了。

   优点：简单易用，插件丰富，部署方便 </br>
   缺点：生成速度非常慢，配置环境麻烦 </br>

3. **Hugo & Gitlab & Firebase**:
   
   > *The world’s fastest framework for building websites.   --HUGO*

   [Hugo](https://gohugo.io/)是由Go语言实现的静态网站生成器，它不想Hexo需要依赖Node.js和nmp去安装各种东西，直接简简单单一个hugo.exe(Windows)搞定，而且就如Hugo网站吹的那样，它的生成速度非常的快，不像`Hexo g -d`那样等半天。[Gitlab](https://about.gitlab.com/)不用说了，和Github类似，主要用其CI/CD，另外Gitlab比Github好在可以被百度爬，但是我们这里只托管源码。实际的网站部署在[Firebase](https://firebase.google.com/)的Hosting上，由于Firebase对移动应用的帮助非常大，谷歌家的东西用起来体验非常的好。但是`firebase login`的验证问题需要梯子，有梯子也不一定能解决:frog:，涉及到这个问题的可以参考这个[Issue](https://github.com/firebase/firebase-tools/issues/155#issuecomment-600966322)(16年的Issue现在还是个谜...)。

   优点：生成速度快，整个流程很方便 </br>
   缺点：国内可能会卡在验证上 </br>

4. **Blogger | CSDN | 简书**:
   
   > *Blogger is a blog-publishing service that allows multi-user blogs with time-stamped entries.   --Wikipedia*
   
   [Blogger](https://www.blogger.com/)、[CSDN](https://www.csdn.net/)和[简书](https://www.jianshu.com/)如果不额外折腾什么样式之类的可以说都是懒人博客了，后两者不用多介绍了。Blogger在2013年被财大气粗的谷歌给买下来了，但是通过Ping `ghs.google.com`可以找到国内可访问IP从而配置成国内可访问的方式。CSDN页面比较乱，简书还好，而Blogger就非常清爽了。

   优点：折腾党可扩展性强，不折腾也勉强能用，直接网页就可以创作 </br>
   缺点：国内开发者贡献的模板少，已有组件少需要自己写一些功能 </br>

<a id="markdown-3-补充说明" name="3-补充说明"></a>
### 3. 补充说明

1. 静态网站生成器：
   
   [Netlify](https://www.netlify.com/)给出了一份[「Static Site Generators for JAMstack Sites」](https://www.staticgen.com/)的清单，可以根据需要和热门程度选择适合自己的静态网站生成器。

2. 静态网站托管平台：
   
   托管平台的话有很多了，国内比较热门的应该就是Github Pages了，目前加入了[Actions](https://github.com/features/actions)从而拥有CI/CD的能力了，配合上[Coding](https://coding.net/) CDN的话也算是功能完善了:snowman:。

   其他的托管平台我比较推荐的有：
   
   * [ZEIT](https://zeit.co/)
   * [Firebase](https://firebase.google.com/)
   * [Netlify](https://www.netlify.com/)

3. 搭建静态博客的教程：
   
   关于搭建静态博客，以上这些静态网站生成器的使用说明和相关教程有非常详细的中文博客叙述，这里就不再赘述了。

   一点建议就是尽量选择CI的方式和带有CMS的托管。

<a id="markdown-三-为什么选择blogger" name="三-为什么选择blogger"></a>
## 三. 为什么选择Blogger

******

<a id="markdown-1-blogger介绍" name="1-blogger介绍"></a>
### 1. Blogger介绍

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/202003191.png" width="70%">
</div>

根据[维基百科Blogger](https://zh.wikipedia.org/wiki/Blogger)的介绍，Blogger.com是由Pyra Labs公司创立，是当前全球用户数量最多的个人网志服务提供商。Pyra Labs和Blogger.com均被Google公司收购，成为其旗下的一项服务内容。

有以下特点：

* Blogger提供免费主机Blogspot.com存放博客，用户不必写任何代码或者安装服务器软件或脚本，通过所见即所得界面轻松地创建、发布、维护和修改自己的网志。

* Blogger允许有经验的用户自行设计博客界面，其模板支持使用HTML和CSS进行编辑。

这非常方便两种人使用Blogger进行博客写作，一种像我一样不怎么会前端也不想折腾的懒人，和"有经验的用户"去自行设计博客界面，正如Blogger网站所介绍的"*Publish your passions, you way.*"。另外提供CMS相对于很多托管实在是方便太多了。

<a id="markdown-2-blogger国内使用问题" name="2-blogger国内使用问题"></a>
### 2. Blogger国内使用问题

由于某些原因，国内无法访问Blogger。但是谷歌拥有全球边缘网络，可以通过一些网络测试工具获取`ghs.google.com`的探测结果，选取合适的IP，将的CNAME解析更改为A解析。比如通过[站长工具](http://tool.chinaz.com/)Ping `ghs.google.com`，可以获得一些可Ping通的国内固定IP，然后选取合适的IP进行测速发现访问可行。

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host@master/Blogger/assets/ghsping.png" width="100%">
</div>

因此，设定好合适的A解析和另外一个CNAME解析后，国内即便没有梯子也可以快速的访问你的博客。

<a id="markdown-3-选blogger的想法" name="3-选blogger的想法"></a>
### 3. 选Blogger的想法

正如前面的叙述，折腾各种博客框架花了我很多的时间，因此我急切寻求一种非常简单的方式去记录一些内容，而且前端的东西乱糟糟的看的我头大:pig:。为此我还在V站发了一个求助帖：[「V 站可以出一个付费的博客频道吗」](https://www.v2ex.com/t/653013#reply21)，但是V站的朋友很多都是技术向选择自建博客，同时得到版主的回应说在考虑建个博客频道但是存在一定顾虑。

诚然很多的博客平台如微软MSN Spaces、网易博客等都相继关停，用博客的人也越来越少了，这本来就是时代的趋势，国内剩下的几个较大的博客平台也就只有[CSDN](https://www.csdn.net/)、[新浪博客](http://blog.sina.com.cn/)等，但是CSDN太偏向于技术，而新浪博客的页面实在是太乱了。

通过翻了V站N个帖子分析了大家的需求和建议后，我最终选择了背靠谷歌的Blogger，作为我的自留地。

以前网站的帖子就不迁移了，重新开始。

<a id="markdown-参考references" name="参考references"></a>
## 参考(References)

******

* [WordPress建站: 便宜VPS+LAMP搭建+博客一键安装教程](https://www.seoimo.com/wordpress-vps/) </br>

* [Hexo + GitHub (Coding) Pages 搭建博客](https://github.com/HarleyWang93/blog/issues/1) </br>

* [Hugo + Firebase + Gitlab 自动化部署你的网站](https://adevjoe.com/post/hosting-with-hugo-firebase/) </br>

* [为什么我使用 Blogger 搭建自己的博客](https://blog.iljw.me/2019/10/why-do-i-use-blogger-to-build-blog.html) </br>