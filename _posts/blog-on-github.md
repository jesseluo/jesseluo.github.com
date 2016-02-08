---
layout: post
title: "在Github上使用Octopress部署自己的博客"
date: 2012-11-23 22:57
categories: 其它技术
tags: [前端, Github, blog, Jekyll, 博客, Octopress]
---

最近这几个月真是动荡不安，连信用卡都丢了。副作用之一就是aws要挂了，原来的博客也就荒废了。长话短说，几经权衡，我现在选择Github Pages + Jekyll作为新博客的方案。其优点有五：  
1. Github服务稳定，可以绑定自己的域名，没有一些蛋疼的备案之类的问题；  
2. 不用管数据库，不用管配置，把精力集中在内容上；  
3. 可以用Markdown编写博客，格式与内容分离，即使本地编写也不用担心格式问题；  
4. 操作简单，尤其是mac上还有Mou这种优秀的md编辑器；  
5. 作为一个二逼文艺程序员，这样的博客显得比较有逼格#@￥#%……  

这里就简单介绍下怎么在Github上使用Octopress部署自己的博客吧。
<!-- more -->
##简介
Jekyll是一个静态网站生成工具。它允许用户使用HTML、Markdown或Textile来建立静态页面，然后通过模板引擎Liquid（Liquid Templating Engine）来运行。  
Jekyll是基于Ruby编写的，所以配置本地环境时候也要先配置Ruby。
Octopress是Jekyll的一套框架，可以用来快速的部署基于github的blog。  

##过程
其实很简单，会一点基础的git知识，再参考[Octopress Setup](http://octopress.org/docs/setup/)就很快能完成了。
需要注意的是若只是为了搭建静态博客，只要在source里修改源码，然后执行：  
	rake generate   # 在_deploy目录中生成网站文件  
	rake preview    # 在http://localhost:4000中预览修改后的网站  
	rake deploy     # 部署生成的网站  

最后只需要push上 _deploy目录就可以了，因为这个小细节没看说明，导致俺重建了好几次git库。  
当然有的人可能希望把网站源码也一并版本化，那再把source也加入git库即可。  

##域名
若是有自己的域名，只需要修改CNAME即可。  
以Godaddy为例：  
1. 登陆后进入左上角的My account，点击Domain上的Launch进入域名管理  
2. 点击需要修改的域名，进入该域名管理
3. 在DNS Manager那栏里选launch，进入DNS管理  
3. 里头有一栏叫CNAME(Alias)的，Quick Add添加一栏  
4. 若是根目录访问则Host填@，否则填写想要用的前缀，如blog等，Points to就填你的XXX.github.com  
5. 在本地文件的source目录下建立一个叫CNAME的文本文件，里头写上你的完整域名即可，如我写的就是blog.jesseluo.me  
6. 部署上github  

##添加分享与评论
Octopress自带有分享与评论模块（disqus），可惜在国内环境不大合适，比如没有微博分享等。所以这里可以把它们替换成国内的插件。  
目前国内流行的分享插件有Jiathis，bShare，百度分享等。个人倒是没什么推荐，随便选了个bShare。如果是希望做一些建站相关的，可以选择百度分享。  
评论插件有友言，多说，灯鹭等，各有千秋。灯鹭应该是功能最强悍的，友言和Jiathis是一家，如果分享用了Jiathis评论就可以用友言。而多说比较好看些，后台也用的顺手。
替换也很简单，先到要使用的插件的网站上把代码取出，修改source/_layout/post.html，把其中和disqus相关的代码替换为多说提供的代码。修改source/_include/post/sharing.html，把不需要的分享代码删除，替换为bShare提供的代码即可。

##其它
Octopress真是个很强悍的框架，生成的博客支持Responsive Web Design，在手机上浏览时候会自动编排为移动终端布局。为了不浪费如此优秀的特性，我们可以为博客添加一个图标。这样若是读者使用iDevice浏览我们的博客时可以把网站的图标作为快捷方式添加到主屏上（虽然估计没什么人干……哈哈）。  
在/source/_includes/head.html中找到如下语句：  
	<meta name="author" content="{{ site.author }}">  

在后面添上：  
	<link rel="apple-touch-icon" href="apple-touch-icon-precomposed.png"/>  

这里的apple-touch-icon-precomposed.png就是主屏图标，我这里用了最偷懒的写法。更具体的写法具体可以参照[这里](http://www.prower.cn/technic/2314/ "iOS中为网站添加图标到主屏幕以及增加启动画面")

另外在github上也可以采用Jekyll Bootstrap作为基本框架来搭建博客。  

##参考
* [用octopress来写博客](http://caok.github.com/blog/2012/06/24/install-octopress-to-write-blog/)
* [Octopress主题集](http://zonyitoo.github.com/blog/2012/04/14/octopresszhu-ti-ji.markdown/)
* [Markdown语法示例](http://equation85.github.com/blog/markdown-examples/)  
* [Github Pages极简教程](http://yanping.me/cn/blog/2012/03/18/github-pages-step-by-step)
