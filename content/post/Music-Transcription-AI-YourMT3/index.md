---
title: "试玩2024地表最强AI扒谱工具YourMT3"
description: 
date: 2024-08-12T12:20:01+08:00
image: https://resources.blog.kihh.xyz/image/YourMT3.png
math: 
license: 
hidden: false
comments: true
draft: false
---

前言：我玩过许多免费、收费的AI扒谱工具，但效果都不尽人意，这篇文章要介绍的工具也是一样图个乐（所以是玩），扒出来也就听个响，毕竟还是AI为辅人工为主，只不过这个模型扒谱的效果相当不错~~得以让我水一篇文章~~

## 体验地址：

Huggingface空间 直接玩：[YourMT3 - a Hugging Face Space by mimbres](https://huggingface.co/spaces/mimbres/YourMT3)

Google Colab：https://colab.research.google.com/drive/1AgOVEBfZknDkjmSRA7leoa81a2vrnhBG

不过Huggingface Space的版本好像只有YPTF.MoE+Multi (noPS)这一个模型可以用，推荐去Colab可以从多个模型里自选

## 效果对比：

我分别使用三款软件分别是**YourMT3（开源 2024）**、**AnthemScore 5（付费 2024）**、 **PianoTrans（ 开源 字节跳动 2022）** 来对 小米晴天闹钟铃声 Alarm_Sunny_Background1 这首纯钢琴曲进行扒谱

#### 音频试听：

原版：

[https://resources.blog.kihh.xyz/file/20240812/Alarm_Sunny_Background1.mp3](https://resources.blog.kihh.xyz/file/20240812/Alarm_Sunny_Background1.mp3)

YourMT3：

[https://resources.blog.kihh.xyz/file/20240812/YourMT3.mp3](https://resources.blog.kihh.xyz/file/20240812/YourMT3.mp3)

AnthemScore 5：

[https://resources.blog.kihh.xyz/file/20240812/AnthemScore 5.mp3](https://resources.blog.kihh.xyz/file/20240812/AnthemScore 5.mp3)

PianoTrans：

[https://resources.blog.kihh.xyz/file/20240812/PianoTrans.mp3](https://resources.blog.kihh.xyz/file/20240812/PianoTrans.mp3)

其中可以很明显的听出AnthemScore 5错误的识别了BPM导致节奏变慢，PianoTrans识别错了最后一小节的音符

（我的错，hugo好像不支持markdown的audio控件，所以只能放链接了，谢谢理解）

#### 谱子展示（仅展示第一行）：

YourMT3：

![](https://resources.blog.kihh.xyz/image/20240812120212.png)

扒出来还是一股AI味，不过效果还不错

AnthemScore 5：

![](https://resources.blog.kihh.xyz/image/20240812120230.png)

全都堆到一个声部，并且bpm还识别错误

PianoTrans：

![](https://resources.blog.kihh.xyz/image/20240812120551.png)

毕竟是22年的产物出点错也情有可原，不能拿来跟AI元年的产物比，不过虽然最后几小节出错但前面都还可以

## 多乐器扒谱：

这款YourMT3和Google MT3（我未部署成功仅看过文档）一样支持多乐器扒谱，但也只是听个响级别，不过整体调子还真能跟原曲大差不差有点震惊到我了

![](https://resources.blog.kihh.xyz/image/20240812121109.png)
