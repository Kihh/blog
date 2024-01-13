---
title: '优化GoogleBlogger博客在国内的访问'
date: 2022-08-11T20:16:00.011+08:00
draft: false
---

GoogleBlogger是谷歌出品的一个免费写博客的网站，本站就托管于Blogger。

Blogger类似国内的博客园、知乎、新浪博客，但我选择Blogger是因为其它平台要么就是自带广告要么就是不好用，审核起来稍微擦点边给你打回去，解析域名还要开通VIP。Blogger相对于这些平台的优点在于可以自己解析域名，可以导入导出文章，可以自己连接谷歌广告赚钱，没有任何外界广告植入，个人体验感觉优于国内平台。

但Blogger终究还是谷歌的，默认的一些资源在国内无法访问，并且写文章的后台还在“外面”，但可以通过优化来解决问题。

[![](https://resources.blog.kihh.xyz/image/321a5a0dc8e956d1fef7d267ca9dcd26.jpeg)](https://resources.blog.kihh.xyz/image/321a5a0dc8e956d1fef7d267ca9dcd26.jpeg)

  

1.优化资源

静态优化：  

主题里的一些js、svg等资源是托管于美国谷歌云的，当然不宜于国内访问，可以通过镜像的方式来优化访问，这里我提供我搭建的两个镜像站，通过cloudflare进行全球访问加速

[https://blogblog.pages.dev](https://blogblog.pages.dev) 对应于 [](https://www.blogblog.com)[](https://www.blogblog.com)[https://](https://blogblog.pages.dev)[www.blogblog.com](http://www.blogblog.com)

[https://resourcesblogblog.pages.dev](https://resourcesblogblog.pages.dev/) 对应于 [https://resources.blogblog.com](https://resources.blogblog.com)

这里直接在编辑html里搜索替换就行，镜像站是反代所有资源的，本站现在自用

有些是不需要处理的，比如www.gstatic.com，本来就能ping通就不需要处理

网上那种改</head></body>标签的不知道是不是我主题不好还是咋的，没用  

图片托管：  

站内图片上传到Blogger托管肯定是不行，因为图片都是直接使用blogger.com域名加载，我建议使用Picgo+Github做图床来让全球访问，这样效果是不错的

评论系统：

猜也知道谷歌的评论系统在国内肯定无法访问，加载不了不说还会拖慢文章加载速度，网上大多教程里提到的系统都已GG，可以参考大多适用于Hexo的Gitalk系统，但个人来说需要Github登录就比较麻烦了，本站启用中  

2.加速绑定的域名

用过的应该都知道Blogger默认域名是被墙的但绑定的域名是可以让国内访问的，但访问速度依然不理想，因为是谷歌云的CDN，但可以固定IP，就是比如将speed.kihh.ml A解析到优选IP，再将blog.kihh.ml CNAME解析到speed.kihh.ml，就能实现blog.kihh.ml解析到的IP是固定、最优的，如图

[![](https://resources.blog.kihh.xyz/image/20220811195325.png)](https://resources.blog.kihh.xyz/image/20220811195325.png)

优选IP如何获得？参考cloudflare全ping一遍的原理，网址：[ping.chinaz.com](https://ping.chinaz.com)

输入ghs.google.com并点击ping检测，查找延迟最小的IP即可

[![](https://resources.blog.kihh.xyz/image/20220811195507.png)](https://resources.blog.kihh.xyz/image/20220811195507.png)

 

3.SEO优化

谷歌的产品谷歌收录是很方便的，但百度估计不太方便，但我看过是有Blogger博客在百度上收录的，这个看运气吧