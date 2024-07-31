---
title: "教你制作一个有逼格的steam动态展柜"
description: 
date: 2024-07-31T21:57:01+08:00
image: https://resources.blog.kihh.xyz/image/20240731215955.png
math: 
license: 
hidden: false
comments: true
draft: false
---

省流+题外话：这个教程会教如何将视频通过动图方式展示在steam主页，展柜是创意工坊展柜，想做一张大动图的那种展柜的话建议去B站找教程，得一个图层一个部位扣并用AE做动效，图文教程很难详细写

效果：[Steam 社区 :: Kihh (steamcommunity.com)](https://steamcommunity.com/id/Kihhh/)

内容可能会换，但逼格一定够高就是（

现在这个视频是我跟朋友闹着玩随便剪来发抖音的，正好拿来当素材

内容是约战狂三外传的OP，找不到原版无字幕OP就只能偷懒拿汉化组版的了

![](https://resources.blog.kihh.xyz/image/20240731215955.png)

### 进入教程

文件大小

1.首先准备好视频和转好的GIF，转GIF可以用这个网站：[Animated GIF Maker (ezgif.com)](https://ezgif.com/maker)

文件不易过大，控制大小在25MB以下最佳，没关系后面也可以压缩调整

参数：宽度800px等比缩放，帧数25帧或更高更低

![](https://resources.blog.kihh.xyz/image/20240731221050.png)

2.将GIF导入Photoshop

**编辑——图像大小** 将宽度改为766，高度会自动等比缩放

<img src="https://resources.blog.kihh.xyz/image/20240731230147.png" style="zoom:67%;" />

**视图——参考线——新建参考线面板**，列为5，装订线4像素

<img src="https://resources.blog.kihh.xyz/image/20240731230322.png" style="zoom:67%;" />

3.使用左侧工具栏将高度拉高1000+，后面再调整，因为直接使用会在展柜存在大黑边

![](https://resources.blog.kihh.xyz/image/20240731230516.png)

4.用剪裁工具按参考线裁剪出五块，每个的宽度都是150

每一块都在 **文件——导出——存储为Web所用格式（旧版）**处保存

这样就得到了五个部分的图像

![](https://resources.blog.kihh.xyz/image/20240731230917.png)

5.使用ultraedit或其他16进制编辑器打开gif文件，将第6 7 8 9列的数值（一般为96 00 xx xx）搜索并全部替换成96 00 af 01（16进制的431，即是原图的高），保存退出

<img src="https://resources.blog.kihh.xyz/image/20240731232029.png" style="zoom:67%;" />

6.如果你的图像大小超过了5MB，是无法在创意工坊上传的，可以在[Animated GIF optimizer and compressor (ezgif.com)](https://ezgif.com/optimize) 这个网站进行压缩，按大小调整压缩力度即可

![](https://resources.blog.kihh.xyz/image/20240731231817.png)

7.准备好压缩完的文件，再次拖入ultraedit或其他16进制编辑器，将最后一位不管什么数值都改为21，否则上传完必有大黑边，别问我怎么知道的，问就是我传过一遍错的（

<img src="https://resources.blog.kihh.xyz/image/20240731232401.png" style="zoom: 67%;" />

8.最后一步，在steam社区上传艺术作品

快捷通道：https://steamcommunity.com/sharedfiles/edititem/767/3

选择完文件在F12控制台输入代码：

```javascript
$J('#ConsumerAppID').val(480),$J('[name=file_type]').val(0),$J('[name=visibility]').val(0);
```

1-5全部上传完后，在我的创意工坊展柜逐个选择即可啦

![](https://resources.blog.kihh.xyz/image/20240731232841.png)
