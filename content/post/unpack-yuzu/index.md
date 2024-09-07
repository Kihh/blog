---
title: "解包柚子社steam国际中文版游戏"
description: 
date: 2024-09-07T21:14:01+08:00
image: https://resources.blog.kihh.xyz/image/102d02da27481348e0cf662472431c4.jpg
math: 
license: 
hidden: false
comments: true
draft: false
---

文章仅供学习交流，侵删

本教程不适用于2023年0721发布的《魔女的夜宴FHD版》，可能采用清单验证之类的更复杂的加密方式，并且这种加密方式可能延续到《天使嚣嚣》和《DRACU-RIOT FHD版》，nekonyan版未测试我也没有（9月8日记：天使的审核再次被打回，可能褒姒了）

众所周知[YUZUSOFT](https://www.yuzu-soft.com/)的游戏steam版本有针对steam api的二次加密，不能通过任何方法对XP3或exe直接解包，这时候就要动点手段移除exe的加密

## 首先要备份存档！备份存档！备份存档！

我第一次搞千恋万花的时候直接炸档了，保存的丛雨CG全没了

存档路径可能如下，用户名自行修改：

C:\Users\Kihh\AppData\Roaming\YuzuSoft

C:\Users\Kihh\AppData\Roaming\Yuzusoft_HIKARIFIELD

### 一、下载工具：

[atom0s/Steamless (github.com)](https://github.com/atom0s/Steamless/releases)

steamless可以移除exe的Steam DRM加密

在1处选择游戏的exe，以parquet为例

若做完教程还是打不开就在3处勾选 Dump SteamDRMP.dll To Disk

<img src="https://resources.blog.kihh.xyz/image/20240908035939.png" style="zoom:50%;" />

点击unpack file，程序会在游戏目录生成xxx.exe.unpacked.exe，这就是移除DRM后的exe

### 二、添加3DM通用steam API DLL

将目录里原来的steam_api.dll或steam_api64.dll添加.bak后缀做备份

再往目录塞一个3DM通用破解DLL

[steam_api.dll补丁下载 _3DM单机 (3dmgame.com)](https://dl.3dmgame.com/patch/103469.html)

dll可能藏在子文件夹，建议搜索一下

### 三、尝试解包

首先尝试打开一下xxx.exe.unpacked.exe，可能会提示让你清除存档，所以开篇先让你备份存档

若能打开，就说明解密成功，可以开始解包了

将exe拖入KRKRDump再把游戏玩一遍即可，老样子
