---
title: "笑谈：1200帧的千恋万花，不锁帧导致的"
description: 
date: 2024-06-22T20:12:55+08:00
image: 
math: 
license: 
hidden: false
comments: true
draft: false
---

最近我在网上刷到一些离谱BUG，有人玩GalGame时GPU一直跑满，一看帧率1000+，其实就是没锁帧而已，我看着挺好玩的，就还原出了这个BUG

<img src="https://resources.blog.kihh.xyz/image/E59A1E8F4202E20995BC230D76FF6620.jpg" style="zoom: 25%;" />

真，第一人称射击游戏

可以看到帧率到达了恐怖的1200帧，GPU占用也是接近吃满的，这还只是一个纸片游戏（



#### 还原方法（谨慎尝试）

打开NVDIA APP——图形——全局设置，关闭BatteryBoost，监视器技术改为固定刷新，关闭垂直同步

![](https://resources.blog.kihh.xyz/image/20240622210537.png)

再打开千恋万花或柚子系游戏——帮助——显示高级设置，再点击右边的高级设置，最大帧速率改为无限制，多线程绘图改为8线程

<img src="https://resources.blog.kihh.xyz/image/20240622210857.png" style="zoom: 67%;" />

<img src="C:\Users\Kihh\AppData\Roaming\Typora\typora-user-images\image-20240622210934993.png" alt="image-20240622210934993" style="zoom:59%;" />

然后重启游戏，就会发现游戏变成了几百帧-1000多帧，如果没用尝试播放一下OP或者其他影片



#### 修复方法

即是还原方法反过来

NVDIA APP——图形——全局设置

可以直接尝试点击右上角“恢复”，若没用就手动操作一下

开启BatteryBoost，监视器技术改为适合你显示器型号的，垂直同步改为使用3D应用程序设置

再打开千恋万花或柚子系游戏——帮助——显示高级设置，再点击右边的高级设置，最大帧速率改为60帧，多线程绘图改为无

