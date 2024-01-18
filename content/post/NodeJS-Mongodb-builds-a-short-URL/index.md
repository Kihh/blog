---
title: 'NodeJS+Mongodb在Vercel上搭建短网址系统，支持API'
date: 2022-08-13T16:49:00.006+08:00
image: https://resources.blog.kihh.xyz/image/20240118231706.png
draft: false
---

最近闲的没事干想整一套易用的短网址系统，国内的不是GG就是付费，国外的谷歌短网址和Git.io已经停运，就想着自建短网址。

最开始我整了个[zun.cab](http://zun.cab)，是利用纯PHP搭建的，没有搞好会留下create.php的请求后缀。

近几天我在逛Github的时候发现了[bihty](https://github.com/bihtyu)[u](https://github.com/bihtyu)大佬的[short-url](https://github.com/bihtyu/short-url)程序，我感觉布局还是挺精美简洁的，就想着整一个。作者没有写项目部署教程，于是我就自己研究了下，还是搭建好了。这是大佬的演示站：[vercel.bihtyu.com](http://vercel.bihtyu.com)，我略修改后部署的网站：[realms.tk](http://realms.tk)（未更改核心部分，仅对前端修改），程序还是支持API的，这里不多介绍

下面介绍下Vercel，Vercel在之前略提过几笔，类似于Heroku，但Vercel更适用于部署网站，免费版每月每个项目有100GB的流量限制，不限运行时间，可以说是比较良心了

Mongodb这里可以自行部署，但在这个教程里我会教大家如何白嫖Mongodb官方出品的免费云数据库，免费配额是共享配置和512MB， 其实空间不小了这里我算过大概能写入87000多条短网址，你自用完全够用，公开估计也够的，站做大了就更换自建

[![](https://resources.blog.kihh.xyz/image/ddf7410c06c81caa45b8bd4ef2299d56.jpeg)](https://resources.blog.kihh.xyz/image/ddf7410c06c81caa45b8bd4ef2299d56.jpeg)

1.注册MongoDB cloud，最近官网有点卡，进不去挂科学通道，网站：[https://account.mongodb.com/account/register](https://account.mongodb.com/account/register)

填写信息后进入邮箱验证即可，然后会让填写一封无聊的调查问卷，随意填写亦可

[![](https://resources.blog.kihh.xyz/image/20220813143837.png)](https://resources.blog.kihh.xyz/image/20220813143837.png)

2.选择最右侧免费的共享计划，点击Create进入集群创建页面

[![](https://resources.blog.kihh.xyz/image/20220813144141.png)](https://resources.blog.kihh.xyz/image/20220813144141.png)

3.下面选择离你近的地区，我选了Azure的香港

[![](https://resources.blog.kihh.xyz/image/20220813144701.png)](https://resources.blog.kihh.xyz/image/20220813144701.png)

  

[![](https://resources.blog.kihh.xyz/image/20220813144846.png)](https://resources.blog.kihh.xyz/image/20220813144846.png)

4.下面两个选项Cluster Tier和Additional Settings保持默认就行，其他都要付费，最下面集群名称是可以自定义且可以重复，写个好看的就行后作子域，当然也可保持默认，之后点Create Clustor创建就行，中间有GG验证码！部署会耗费一会时间  

[![](https://resources.blog.kihh.xyz/image/20220813145433.png)](https://resources.blog.kihh.xyz/image/20220813145433.png)

5.之后创建一个关于数据库的用户名密码，之后有大用保存好！

[![](https://resources.blog.kihh.xyz/image/20220813145844.png)](https://resources.blog.kihh.xyz/image/20220813145844.png)

6.下面是设置可读写的IP，我没有研究过MongoDB的权限问题，看网上说填写0.0.0.0/0是可以公开访问的，这里照做，我的站也是这么做的，之后点击Add Entry添加  

[![](https://resources.blog.kihh.xyz/image/20220813150040.png)](https://resources.blog.kihh.xyz/image/20220813150040.png)

7.然后回到主页，点击Connect，选择Connect your application，不用动别的选项先复制下mongodb+srv://开头的连接地址，更改链接中的<password>为你上一步设置的密码

[![](https://resources.blog.kihh.xyz/image/20220813150857.png)](https://resources.blog.kihh.xyz/image/20220813150857.png)

现在数据库这边的准备工作做完了，来配置下  

8.进入大佬的Github程序主页并Fork一份：[bihtyu/short-url](https://github.com/bihtyu/short-url) 

9.修改/DB/config.js中的信息，将mongodb+srv://开头的那一串数据都改成刚才复制的，下面的DB\_NAME要创建的数据库名称随意，可以改成你喜欢的，比如我改成了url

[![](https://resources.blog.kihh.xyz/image/20220813151458.png)](https://resources.blog.kihh.xyz/image/20220813151458.png)

程序这边也配置完了，接下来部署在Vercel上  

10.注册Vercel，网站：[https://vercel.com/signup](https://vercel.com/signup)，使用Github注册，后期方便部署

[![](https://resources.blog.kihh.xyz/image/20220813142603.png)](https://resources.blog.kihh.xyz/image/20220813142603.png)

11.回到Vercel，点击右上角New Project

[![](https://resources.blog.kihh.xyz/image/20220813142904.png)](https://resources.blog.kihh.xyz/image/20220813142904.png)  

12.选择你刚刚Fork的仓库，点击右边Import

[![](https://resources.blog.kihh.xyz/image/20220813151732.png)](https://resources.blog.kihh.xyz/image/20220813151732.png)

（这边名称有个锁是因为我怕数据库会暴露在外面所以下载下来创建私有仓库传上去）  

13.接下来进入设置页面，这里最好别动，虽然Project Name后面是做子域的，但都搞短网址了就不需要系统自带域名，点击Deploy部署

[![](https://resources.blog.kihh.xyz/image/20220813152217.png)](https://resources.blog.kihh.xyz/image/20220813152217.png)

14.然后等蹦出Html5特效烟花就是部署完了，现在你的短网址网站已经可以访问了，在项目页面中间的Domains中有一个系统自带域名XXX.vercel.app可以访问，但有亿点长（对于短网址），接下来自定义域名

进入项目页面点击sittings，然后点击左侧domains

[![](https://resources.blog.kihh.xyz/image/20220813152539.png)](https://resources.blog.kihh.xyz/image/20220813152539.png)

15.在框中输入你的域名，点击右侧add，我推荐选择第三个方式，前两个重定向太麻烦也用不到

[![](https://resources.blog.kihh.xyz/image/20220813153322.png)](https://resources.blog.kihh.xyz/image/20220813153322.png)

[![](https://resources.blog.kihh.xyz/image/20220813153918.png)](https://resources.blog.kihh.xyz/image/20220813153918.png)

16.然后根据给出的IP去自己的平台解析就行

[![](https://resources.blog.kihh.xyz/image/20220813162336.png)](https://resources.blog.kihh.xyz/image/20220813162336.png)

  

17.之后等待10-15分钟自动申请一个Let's Encrypt的证书后就能访问了

[![](https://resources.blog.kihh.xyz/image/20220813162826.png)](https://resources.blog.kihh.xyz/image/20220813162826.png)

FAQ：

生成短链出现Error：

数据库权限错误，检查填写的库是否已存在或存储空间是否已满  

生成短链出现bad auth : Authentication failed：

数据库用户名密码错误，检查用户名和密码