---
title: "解除光猫公网IPV6防火墙，适用于远程和开服等"
description: 
date: 2024-02-17T00:14:04+08:00
image: 
math: 
license: 
hidden: false
comments: true
draft: false
---

家里之前整了台12核32G的”家里云“服务器，一直在想怎么对服务器进行公网操作，因为现在普通家宽根本就拿不到公网IPV4，电信客服总是以IPV4不足的理由不给开通，但客服告诉了我IPV6是公网，我早几年前就拿Cloudflare试过套V6建站行不通，我想是不是防火墙的原因，于是最近就开始研究

我的设备信息：

> 设备类型
>
> EPON天翼网关（无WiFi）
>
> 产品型号
>
> TEWA-707E

我打电话给宽带师傅拿到了超级管理员密码，在http://192.168.1.1:8080/login.html成功登录

![](https://resources.blog.kihh.xyz/image/20240217002349.png)

接着，给光猫开通telnet，地址：http://192.168.1.1:8080/enableTelnet.html

输入密码并点击“使能telnet“，然后点右下角的”确定/应用“

FTP也是在此处开通，刷固件可以使用FTP

![](https://resources.blog.kihh.xyz/image/20240217002715.png)

然后，telnet连接到192.168.1.1，这里我使用putty连接，因为cmd连接telnet时不能上下翻历史输出

![](https://resources.blog.kihh.xyz/image/20240217002924.png)

在连接后在命令行中输入用户名和密码，成功连接！

![](https://resources.blog.kihh.xyz/image/20240217003213.png)

使用ip6tables命令来对防火墙进行操作

查询所有IPV6防火墙规则

```shell
ip6tables -nvL --line-number
```

输出了一大截东西，还是让GPT帮咱分析一下吧

> 这是一个比较复杂的IPv6防火墙规则设置。让我为您分析每个链中的规则：
>
> ### Chain INPUT
>
> - **ACCEPT ipv6-icmp**: 允许来自任何源地址和目标地址的IPv6 ICMP流量，ICMP类型为130。
> - **MacFilter**: 应用了某种Mac地址过滤规则。
> - **ddos**: 用于处理DDoS攻击的规则。
> - **input_wanlocal**: 从WAN接口进入的本地流量的规则。
> - **input_advance**: 高级输入规则。
> - **input_firewall**: 输入防火墙规则。
>
> ### Chain FORWARD
>
> - **ACCEPT all**: 允许从任何源地址到`ff00::/8`的IPv6流量。
> - **app_filter**: 应用了应用程序过滤规则。
> - **MacFilter**: 应用了Mac地址过滤规则。
> - **ipaddrfilter**: 应用了IP地址过滤规则。
> - **mwband**: 处理带宽限制的规则。
> - **rtchain**: 路由链规则。
> - **tcpmss**: 处理TCP MSS（最大分段大小）的规则。
> - **urlfilter**: 应用了URL过滤规则。
> - **urlfilter_dbus**: 应用了URL过滤规则。
>
> ### Chain OUTPUT
>
> - **output_firewall**: 输出防火墙规则。
>
> 此外，还有一些其他的链，例如`MacFilter`，`NODATA_ACK_SKIP_SET_MARK`，`SAMBA_IN`，`ftp_telnet`，`hardacc_cancel`，`http_web`，`ipaddrfilter`，`urlfilter_http`等。这些链可能是用于更特定目的的自定义规则。

经过我的研究，应该是forward_firewall中DROP all anywhere anywhere这条规则阻止了所有的转发流量

```
Chain forward_firewall (1 references)  numbtarget  prot  opt  source  destination
1    ACCEPT  ipv6-icmp  anywhere  anywhere  ipv6-icmp echo-request limit: avg 8/sec burst 5 
2    ACCEPT   all  anywhere  anywhere   ctstate RELATED,ESTABLISHED 
3    LOG   tcp   anywhere   anywhere   tcp flags:FIN,SYN,RST,ACK/SYN limit: avg 6/hour burst 5 LOG level alert prefix "Intrusion -> " 
4    DROP   all   anywhere   anywhere
```

删除这条规则

注：请根据实际情况调整规则的编号，我这里编号为4

```shell
ip6tables -D forward_firewall 4
```

再用IPV6多地PING工具www.itdog.cn/tcping_ipv6/进行测试，全绿！

注：此工具需要一个已运行服务的端口才能测试，我开了两个Minecraft服务端测试25565和25585端口

![](https://resources.blog.kihh.xyz/image/20240217011257.png)

回到我的问题，是否封闭了80和443端口？

使用wampserver运行网页服务，本地正常访问

![](https://resources.blog.kihh.xyz/image/20240217013840.png)

在异地的服务器上无法访问，并且多地ping80端口也无法ping通

![](https://resources.blog.kihh.xyz/image/20240217014032.png)

说明服务商不开放80和443端口，这也是意料之中的

不用时记得重启光猫即可重置为原有规则，使网络变得更加安全