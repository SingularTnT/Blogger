## W. Liu's blog

Project面向Blogger创作，通过Github仓库储存和管理文件，包括：

* post: 发布的博文及页面
* static_files: 静态文件(JavaScript、CSS等)
* xml: 备份和更新的主题背景文件

实现方式包括：

* 写作：通过[Typora](https://typora.io/)及[VSCode](https://code.visualstudio.com/)写作，或者直接在Blogger上通过Markdown写作，使用Chrome的[Markdown-here](https://markdown-here.com/)插件编译成html
* 发布：使用[StackEdit](https://stackedit.io/)发布至[Blogger](https://www.blogger.com/)上
* 图床：通过[PicGo](https://github.com/Molunerfinn/PicGo)将图片上传至GitHub仓库，然后通过[jsDelivr](https://www.jsdelivr.com/)的CDN加速访问
* 评论：评论系统目前采用[来必力](https://livere.com/)实现，但是由于加载过慢，后续考虑更换[Valine](https://valine.js.org/)代替
* 对象存储：采用[腾讯云OSS](https://cloud.tencent.com/)存储JS等文件
* 域名：通过[腾讯云](https://cloud.tencent.com/)注册，同时通过腾讯云后台进行解析，解析Blogger的IP通过Ping工具寻找"ghs.google.com"的国内可用IP进行A解析，另外一个直接用CNAME即可，后续考虑更换[Cloudflare](https://www.cloudflare.com/)
* HTTPS：Blogger后台已经原生支持HTTPS，直接打开即可

各类工具：

VSCode
* Markdown All in One: 预览Markdown和生成TOC
* Markdown PDF: 转换.md为html