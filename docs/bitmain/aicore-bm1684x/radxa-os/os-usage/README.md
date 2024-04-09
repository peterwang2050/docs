---
sidebar_position: 2
sidebar_label: 系统使用
title: 系统使用
---

import Serial from "../../../../common/general/\_serial.mdx"

主要介绍 radxa-aicore-bm1684x OS 系统的基本使用方法，帮助你快速了解常用的系统的配置。

## 用户名和密码

BM1684X默认添加的用户名和密码为：

```
用户名：linaro/admin
密码：  linaro/admin
```

## 串口登录

使用USB 转 UART 线，波特率：115200,用户名和密码如上面介绍

## 设置网络

### 以太网连接

fogwise bm168m整机有两个以太网口，etho是WAN口，默认为DHCP。eth1是LAN口，默认设置为静态IP：192.168.150.1。检查 IP 地址请使用 ifconfig 或 ip a。

## 远程登录

### SSH 登录

在连接上网络后可以通过 SSH 远程调试，官方Debian 镜像已默认开启 SSH ,只需要获取到板子的 IP 即可使用 SSH 连接。

- Debian/Ubuntu

```
ssh [username]@[hostname]
or
ssh [username]@[IP address]
例如：
ssh linaro@192.168.1.100
输入用户密码后即可连接到Debian系统。
```

- Windows

Windows 有许多 SSH 工具，这里以 [Mobaxterm](https://mobaxterm.mobatek.net/) 为你展示连接方法

点击左上角的 `Session` 新建 SSH 连接，在 `Remote host` 处输入板子的 IP，勾选 `Specify usernema` 并填入登录的用户, 双击会话开始连接后输入登录密码即可连接。

![mobaxterm ssh ](/img/zero/zero3/mobaxterm-ssh.webp)
