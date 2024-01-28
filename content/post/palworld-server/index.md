---
title: "在Ubuntu/Debian上部署Palworld幻兽帕鲁服务端"
description: 
date: 2024-01-28T16:08:08+08:00
image: 
math: 
license: 
hidden: false
comments: true
draft: false
---

本教程使用的服务器为阿里云2核2G轻量云服务器，配置比较低很容易崩溃坏档，仅作测试开服使用，推荐配置为4核16G以上，下个教程我会使用我的高配Windows服务器进行开服

首先在服务器防火墙放通服务端所需的8211端口，然后进入教程

### 1、新建一个用户

#### 1.1 服务端无法使用root用户运行，若尝试运行会报错：

`Shutdown handler: initalize.`

`Refusing to run with the root privileges.`

所以要**新建一个用户**

```shell
useradd -m steam
passwd steam
```

#### 1.2 赋予用户sudo权限

#### 1.2.1 编辑sudoers

```shell
vim /etc/sudoers
```

如下图所示在root一行下方添加命令，编辑完后保存并退出

```shell
steam	ALL=(ALL:ALL) ALL
```

![](https://resources.blog.kihh.xyz/image/20240128170425.png)

#### 1.3 登录用户

```shell
su steam
```

#### 1.4 进入用户目录

```shell
cd /home/steam
```

### 2、安装ASCF

若你的服务器在中国大陆，你可能需要安装[AnotherSteamCommunityFix](https://github.com/makazeu/AnotherSteamCommunityFix)来加速对steam的访问，若不是请跳过此步骤

#### 2.1 更新软件源

```shell
sudo apt-get update
```

#### 2.2 安装screen unzip

```shell
sudo apt install screen unzip -y
```

#### 2.3 下载ASCF（因Github被墙原因博主将文件托管于本站的对象存储）

```shell
wget -O https://resources.blog.kihh.xyz/file/ascf_v1.2.2_Linux_x64.zip 
```

#### 2.4 解压ASCF

```shell
unzip ascf_v1.2.2_Linux_x64.zip
```

#### 2.5 给予文件权限

```shell
chmod 755 ascf
```

#### 2.6 让ASCF在后台运行

```shell
screen -dmS ascf sudo ./ascf
```

ASCF会占用系统443端口，因此请检查端口是否被网站占用，不需要时请执行下方命令结束ASCF的screen后台会话

```shell
screen -S ascf -X quit
```

### 3、安装steamcmd

#### 3.1 更新软件源

```shell
sudo apt update
sudo apt upgrade
```

#### 3.2 安装steamcmd

#### 3.2.1 安装依赖项

添加依赖包

```shell
sudo dpkg --add-architecture i386
```

更新软件源

```shell
sudo apt update
```

安装依赖项

```shell
sudo apt install lib32gcc-s1 lib32stdc++6
```

#### 3.2.2 下载安装steamcmd

创建目录

```shell
mkdir steamcmd && cd steamcmd
```

下载并解压

```shell
wget https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz && tar -xvzf steamcmd_linux.tar.gz
```

#### 3.2.3启动steamcmd

```shell
./steamcmd.sh
```

### 4、下载服务端

#### 4.1 匿名模式登录

```shell
login anonymous
```

#### 4.2 下载服务端

```shell
app_update 2394010
```

#### 4.3 下载服务端依赖

```shell
app_update 1007
```

#### 4.4 退出SteamCMD

```shell
quit
```

### 5、创建库链接

#### 5.1 创建.steam文件夹

```shell
mkdir ~/.steam
```

#### 5.2 创建sdk64文件夹

```shell
mkdir ~/.steam/sdk64
```

#### 5.3 创建库链接

```shell
cp ~/Steam/steamapps/common/Steamworks\ SDK\ Redist/linux64/steamclient.so ~/.steam/sdk64/
```

上面的命令是官网技术指南上给出的，但我执行后会报错，原因是我的目录名称与官方给出的不一样，若你执行也出错可以尝试我的目录对应的命令

```shell
cp ~/Steam/steamapps/common/'Steamworks SDK Redist'/linux64/steamclient.so ~/.steam/sdk64/
```

### 6.启动Palworld服务端

#### 6.1进入目录

```shell
cd ~/Steam/steamapps/common/PalServer
```

#### 6.2启动Palworld服务端

```shell
./PalServer.sh
```

### 7.连接Palworld服务器

加入多人游戏（专用服务器）下方输入IP:8211然后点联系即可进入服务器

![](https://resources.blog.kihh.xyz/image/20240128184236.png)

#### 创建一个角色就能开始游玩了

![](https://resources.blog.kihh.xyz/image/20240128183159.png)