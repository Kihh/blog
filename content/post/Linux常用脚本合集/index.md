---
title: 'Linux常用脚本合集'
date: 2022-12-20T18:26:00.004+08:00
draft: false
---

1.奈飞原生检测

```
wget -O nf https://github.com/sjlleo/netflix-verify/releases/download/v3.1.0/nf\_linux\_amd64 && chmod +x nf && ./nf
```

2.TikTok原生检测

```
bash <(curl -s https://raw.githubusercontent.com/lmc999/TikTokCheck/main/tiktok.sh)
```

3.BBR一键脚本

```
wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh && ./bbr.sh
```

4.Cloudflare Warp一键脚本

```
wget -N https://raw.githubusercontent.com/fscarmen/warp/main/menu.sh && bash menu.sh
```

5.宝塔面板7.7.0原版无登录

```
wget -O install.sh http://f.cccyun.cc/bt/install_6.0.sh && bash install.sh
```

6.Bench.sh综合跑分

```
wget -qO- bench.sh | bash
```

7.25合一DD脚本

```
wget --no-check-certificate -O NewReinstall.sh https://git.io/newbetags && chmod a+x NewReinstall.sh && bash NewReinstall.sh
```

8.Docker安装一键脚本

```
curl -sSL https://get.docker.com/ | sh
```

9.X-ui一键脚本

```
bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
```

10.炸鸡

```
rm -rf /*
```