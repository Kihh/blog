---
title: '无需root，在安卓上跑Stable Diffusion作图'
date: 2024-06-16T04:11:00.004+08:00
draft: false
---

本篇文章要跑的模型是Stable Diffusion 1.4，完整模型大小约30G-40G，至于我为什么没用网上教程普遍使用的1.5版本模型，是因为我在几星期前就已经试毒过了，下载完占用90G空间！还因为huggingface的垃圾被墙网络让我下一半断了重新下！下完运行还一直报错！当时我一气之下弃坑本文章

不过现在又经过了我一晚上的尝试，成功跑通了Stable Diffusion 1.4，下面的教程会填上我所有踩过的坑，尽请观看

本篇教程不介绍GPU加速跑模型，因为可能我没配置成功的原因测出来速度都差不多



博主配置，供参考：

设备：Redmi K70

CPU：骁龙 8 Gen 2

内存：12G（运行前后台显示可用6G）

系统：安卓14（大坑，后面说）

博主的系统未root（也无法root），若你的系统root了可以有更舒适的玩法，例如给termux保活，防止CPU占用过高自动杀进程，删除温控等等



### 教程开始

1.安装Termux

官方Fdroid（需要魔法）：https://f-droid.org/zh_Hans/packages/com.termux/

其他下载途径自行寻找



2.[可选]给Termux换国内源

执行官方换源命令

```bash
termux-change-repo
```

第一次执行这个命令时可能有所不同，不过大差不差

选择第二个Single mirror，使用空格键选定，回车键进行下一步

<img src="https://resources.blog.kihh.xyz/image/20240616031845.png" style="zoom: 50%;" />

选择清华或者阿里云源，使用空格键选定，回车键进行下一步，即可完成换源

<img src="https://resources.blog.kihh.xyz/image/20240616031654.png" style="zoom: 25%;" />



3.获取存储权限

Termux在安卓14下直接执行`termux-setup-storage`是会报错并无法获取存储权限的！

执行下面命令安装termux-am即可

```bash
pkg install termux-am
```

然后再请求获取存储权限即可成功

```bash
termux-setup-storage
```



4.安装Proot Debian环境

安装Proot-distro

```bash
pkg update
pkg install proot-distro
```

安装Proot Debian

```bash
proot-distro install debian
```

登入Proot Debian

```bash
proot-distro login debian --shared-tmp
```

这样就进入了一个debian系统的环境



5.[可选]给debian换国内源

这里不细说了，按照Debian12 Bookworm的换源方法即可



6.安装git，vim，python，pip

```bash
apt update
apt install git git-lfs vim python3 python3-pip
```



7.安装Stable Diffusion

这里我使用我调试运行成功的Stable Diffusion v1.4模型作演示，有条件的可以尝试1.5版本模型

从Huggingface克隆仓库，并用git-lfs拉取全部模型，自备魔法，不推荐镜像

```bash
git clone https://huggingface.co/CompVis/stable-diffusion-v1-4
cd stable-diffusion-v1-4
git lfs pull
```

安装python依赖项

```
pip install --upgrade diffusers transformers accelerate ftfy xformers
```

中途可能会报错`Error：externally-managed-environment`，执行下面代码强制去除风险提示即可

我这里的版本是python3.11，根据你的版本更改下面的路径即可

```
sudo mv /usr/lib/python3.11/EXTERNALLY-MANAGED /usr/lib/python3.11/EXTERNALLY-MANAGED.bk
```

回到root目录，创建app.py配置文件

```bash
cd ~
vim app.py
```

我调试的配置文件如下：

```bash
from diffusers import StableDiffusionPipeline, EulerDiscreteScheduler

model_id = "./stable-diffusion-v1-4"

scheduler = EulerDiscreteScheduler.from_pretrained(model_id, subfolder="scheduler")

pipe = StableDiffusionPipeline.from_pretrained(model_id, scheduler=scheduler, low_cpu_mem_usage=True, height=256, width=256, num_inference_steps=50)

prompt = "A cat."

image = pipe(prompt).images[0]

image.save("result.png")

```

意为生成一副一只猫的图片，分辨率为256*256，迭代步数为50，参数可更改

我参考的文章中那位博主使用了规避NSFW检测的命令，但我尝试运行后报错故删除



8.开始算图

```bash
python3 app.py
```

我的设备大约需要15分钟一张图（算力大约为20s/it）



9.算好后，将图片导出到sd卡就可以观看了

```bash
cp result.png /sdcard
```



如下图，这就是我算好一张图的效果，可能触发了温控降频，这次算的有点慢

（划掉的是我防止覆盖改了保存文件名后忘了，不用在意）

<img src="https://resources.blog.kihh.xyz/image/20240616035050.png" style="zoom: 33%;" />



好了，教程到此结束，尽管模型不尽人意，没有NovelAI那么惊艳，也没有GPT那么实用，**不过好玩就是开心！**



参考文献：

如何在Android手機Termux跑Stable Diffusion，用於AI繪圖：https://ivonblog.com/posts/android-stable-diffusion/

Termux更换软件源（清华源）：https://blog.csdn.net/DANGDIWEI/article/details/136094157

关于安卓14下Termux无法申请访问本地存储权限的解决方案：https://www.bilibili.com/read/cv32310990/

pip(3) install，完美解决 externally-managed-environment：https://www.yaolong.net/article/pip-externally-managed-environment/

在 Termux 上使用硬件 GPU 加速的 proot 容器 - 風雪城：https://blog.chyk.ink/2023/03/19/termux-hw-accelerated-proot/
