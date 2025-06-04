---
sidebar_position: 2
---

# 快速上手

本章节的目的是为了让大家快速使用 Radxa ROCK 4D，大家可以按照该教程进行操作。

## 产品实物

<div style={{textAlign: 'center'}}>
   Radxa ROCK 4D 正面
   <img src="/img/rock4/4d/rock4d-top.webp" style={{width: '100%', maxWidth: '1200px'}} />
   Radxa ROCK 4D 背面
    <img src="/img/rock4/4d/rock4d-bottom.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

## 使用前提

### 硬件设备

您需要提前准备以下硬件设备，以便完成快速上手教程的所有操作。

- 开发板： Radxa ROCK 4D
- 系统启动介质：MicroSD 卡
- USB串口数据线（可选）：用于串口调试和登录
- 显示器（可选）：HDMI 显示器和 HDMI 数据线
- 电源适配器：Type-C 电源适配器( 支持 PD 协议，5V 电源输入，建议电流 3A 以上)

**说明**：用户需要在 USB串口数据线和显示器二选一，我们优先推荐使用显示器搭配Rock 4D进行使用和开发。

:::tip
对于不同开发能力的用户，我们建议额外增加以下配件使用 Radxa ROCK 4D，这样会缩短熟悉产品和开发的时间。

- **初学者**

准备配件：电源适配器、系统启动介质、显示器、HDMI数据线

- **开发者**

准备配件：电源适配器、系统启动介质、调试数据线( USB串口数据线)

**说明**：其中显示器可以显示系统界面和进行图形化操作！
:::

### 主板供电

Radxa ROCK 4D 主板支持 Type-C 和 GPIO 供电，我们推荐使用 Type-C 电源适配器供电，请确保电源适配器能够提供 5V 电源输入，并且能够兼容 PD 协议。

:::tip
Radxa ROCK 4D 主板仅支持 5V 电源输入，建议电流 3A 以上，确保所有外设稳定运行。

参考电源：

- [瑞莎 PD 30W电源适配器(推荐使用)](https://radxa.com/products/accessories/power-pd-30w)

- 标准 Type-C 电源适配器( 5V 电源输入，支持 PD 协议，建议电流 3A 以上)
  :::

### 系统启动介质

Radxa ROCK 4D 支持 MicroSD 卡、NVME、UFS启动，但是快速上手教程只介绍 MicroSD卡启动。

### 串口调试

Radxa ROCK 4D 主板支持通过 USB 串口数据线进行串口调试，您需要将 USB 串口数据线连接到 Radxa ROCK 4D 的 UART0_TX、UART0_RX 和 GND 引脚。

## 写入系统镜像

您需要在 PC 上下载待写入的系统镜像文件，并将其烧写到 MicroSD 卡中。

### 下载系统镜像

在 PC 上访问[资源下载汇总](../download)页面，下载 Radxa ROCK 4D 对应的系统镜像压缩包，下载完成后解压系统镜像压缩包，得到的 `*.img` 文件就是待烧写到 MicroSD 卡中的系统镜像文件。

:::tip
下载的系统镜像是一个压缩文件，需要解压后才能通过镜像烧录软件写入到SD卡, 未解压就直接烧录到SD卡，可能会出现写入系统失败或者启动系统失败的情况。
:::

### 写入系统镜像

将 MicroSD 卡插入读卡器中，然后将读卡器插入 PC 的 USB 端口上。

<div style={{textAlign: 'center'}}>
  <img src="/img/rock4/4d/sd-insert.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

- **镜像烧录软件：Balena Etcher**

我们推荐使用瑞莎合作伙伴 Balena 开发的开源镜像烧录工具 Etcher，该软件使用简单，功能强大，支持 Windows/Linux/MacOS 系统使用。

进入官网下载系统对应平台的软件：[balenaEtcher](https://etcher.balena.io)

<div style={{textAlign: 'center'}}>
<img src="/img/rock4/4d/down-etcher-01.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

进入下载页面后，选择对应的系统平台进行 Etcher 软件下载。

<div style={{textAlign: 'center'}}>
<img src="/img/rock4/4d/down-etcher-02.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

:::tip
Windows 和 Linux 只需要打开对应程序就可以使用，无需安装！
:::

<div style={{textAlign: 'center'}}>
  <img src="/img/rock4/4d/down-etcher-00.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

- 安装系统镜像

1. 选择主板对应的系统镜像：点击 `Flash from file` 选项，选择自己提前下载并解压好的系统镜像文件。

<div style={{textAlign: 'center'}}>
  <img src="/img/rock4/4d/etcher-01.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

2. 选择 MicroSD 卡对应的磁盘：点击 `Select target` 选项，选择自己接入 PC 的读卡器对应磁盘设备。

:::danger
请勿选错磁盘，否则 Etcher 将格式化被选中的磁盘，造成重要数据丢失！
:::

<div style={{textAlign: 'center'}}>
  <img src="/img/rock4/4d/etcher-02.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

① ： 选择需要安装系统镜像的磁盘设备

② ： 点击 `Select 1` 选项确认设备选择

<div style={{textAlign: 'center'}}>
  <img src="/img/rock4/4d/etcher-03.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

3.开始写入系统镜像：点击 `Flash` 选项，等待软件自动进行系统镜像的写入和校验。

<div style={{textAlign: 'center'}}>
  <img src="/img/rock4/4d/etcher-04.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

<div style={{textAlign: 'center'}}>
等待系统写入完成
  <img src="/img/rock4/4d/etcher-05.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

<div style={{textAlign: 'center'}}>
等待系统校验完成
  <img src="/img/rock4/4d/etcher-07.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

4.成功写入系统镜像后，关闭 Etcher 软件！

## 系统信息

您使用我们提供的系统镜像，首次需要使用我们设置的用户名和密码登录系统。

- Debian Linux

用户账号：radxa

用户密码：radxa

## 启动系统

在 MicroSD 卡上完成系统镜像的写入后，我们可以将读卡器上的 MicroSD 卡装入 Radxa ROCK 4D 的 MicroSD 卡槽中，然后使用 5V Type-C 电源适配器启动系统。

启动系统后，蓝色和绿色 LED 灯会同时亮起，大概过几秒左右，绿灯常亮、蓝色指示灯会闪烁，一般表示系统启动成功。

使用系统建议：

1. 若您有显示器，启动 Radxa ROCK 4D 后可以使用 HDMI 数据线连接显示器和主板，直接通过显示器查看系统界面。

2. 若您没有显示器，可以使用串口调试工具查看系统输出信息，确认系统是否启动成功以及登录系统使用 Radxa ROCK 4D。

## 串口登录系统

:::tip

- Radxa ROCK 4D 串口参数

波特率：1500000

数据位：8

停止位：1

无校验位

:::

- 硬件连接

:::danger
使用 USB 串口数据线和 Radxa ROCK 4D 进行串口调试时，请确保引脚连接正确，否则会导致主板硬件损坏。
:::

使用 USB 串口数据线的 USB 接口连接 PC ，另一端连接 Radxa ROCK 4D 的 GPIO串口 引脚。

| 序号 | 引脚功能                          | 连接方式                            |
| ---- | --------------------------------- | ----------------------------------- |
| ①    | Radxa ROCK 4D : GND（Pin6）       | 连接 USB 串口数据线的 GND 引脚      |
| ②    | Radxa ROCK 4D : UART0_TX（Pin8）  | 连接 USB 串口数据线的 RX 引脚       |
| ③    | Radxa ROCK 4D : UART0_RX（Pin10） | 连接 USB 串口数据线的 TX 引脚       |
| ④    | USB 串口数据线 : GND（黑色线）    | 连接 Radxa ROCK 4D 的 GND 引脚      |
| ⑤    | USB 串口数据线 : RX（白色线）     | 连接 Radxa ROCK 4D 的 UART0_TX 引脚 |
| ⑥    | USB 串口数据线 : TX（绿色线）     | 连接 Radxa ROCK 4D 的 UART0_RX 引脚 |
| ⑦    | USB 串口数据线 : VCC（红色线）    | 不连接                              |

<div style={{textAlign: 'center'}}>
  引脚说明和连接示意图
  <img src="/img/rock4/4d/serial-connect.webp" style={{width: '80%', maxWidth: '1200px'}} />
</div>

<Tabs queryString="e24c-system-login">

<TabItem value="Windows">

Windows 平台推荐使用 PuTTY 软件串口登陆 Radxa ROCK 4D 系统。

- PuTTY使用

Radxa ROCK 4D 和 PC 通过 USB 串口数据线连接后，可以进入系统的设备管理器查看 Radxa ROCK 4D 对应的串口号(示意图中 COM4 就是当前系统中对应的 Radxa ROCK 4D 设备)。

<div style={{textAlign: 'center'}}>
  <img src="/img/rock4/4d/serial-01.webp" style={{width: '80%', maxWidth: '1200px'}} />
</div>

:::tip

若系统无法正确识别设备或者设备前面带有感叹号，需要自行安装[CH340驱动](https://www.wch.cn/downloads/CH341SER_EXE.html)，完成安装后重启系统。

:::

- 串口登陆选项

① --> Connection type：选择 `Serial`

② --> Serial line：填写 `COM4` (根据设备管理器显示的串口号信息)

③ --> Speed：填写 `1500000`

④ --> Open：串口连接 Radxa ROCK 4D 系统

<div style={{textAlign: 'center'}}>
  <img src="/img/rock4/4d/serial-02.webp" style={{width: '80%', maxWidth: '1200px'}} />
</div>

- 登陆系统

终端内按回车会出现登陆信息，然后使用对应系统的用户账号和密码进行登陆。

终端输入密码不会显示出来，输入完密码按回车登陆。

<div style={{textAlign: 'center'}}>
  <img src="/img/rock4/4d/serial-03.webp" style={{width: '100%', maxWidth: '1200px'}} />
</div>

</TabItem>

<TabItem value="Linux">

Linux 推荐使用 Screen 软件串口登陆 Radxa ROCK 4D 系统。

- 安装Screen

<NewCodeBlock tip="Linux-host$" type="host">
```
sudo apt update
sudo apt install screen
```
</NewCodeBlock>

- 查找串口设备

打开终端使用 ls 命令查看串口设备:

若 PC 只有一个串口设备，系统默认是 ttyUSB0；

若 PC 有多个串口设备，可以插拔 USB 设备，使用下面命令观察变化的设备号。

<NewCodeBlock tip="Linux-host$" type="host">
```
ls /dev/ttyUSB*
```
</NewCodeBlock>

- 串口登陆选项

使用 Screen 连接串口，只需要设置串口号和波特率。

<NewCodeBlock tip="Linux-host$" type="host">
```
sudo screen /dev/ttyUSB0 1500000
```
</NewCodeBlock>

- 登陆系统

终端内按回车会出现登陆信息，然后使用对应系统的用户账号和密码进行登陆。

终端输入密码不会显示出来，输入完密码按回车登陆。

</TabItem>

<TabItem value="MacOS">

MacOS 平台推荐使用 Screen 软件串口登陆 Radxa ROCK 4D 系统。

:::tip

若系统无法正确识别设备，需要自行安装[CH340驱动](https://www.wch.cn/downloads/CH341SER_MAC_ZIP.html)，完成安装后重启系统。

:::

- 查找串口设备

打开终端使用 ls 命令查看串口设备:

找到类似 /dev/tty.wchusbserial14xx0 的设备名称，若 PC 有多个串口设备，可以插拔 USB 设备，使用下面命令观察变化的设备号。

<NewCodeBlock tip="MacOS-host$" type="host">
```
ls /dev/tty.*
```
</NewCodeBlock>

- 串口登陆选项

使用 Screen 连接串口，只需要设置串口号和波特率。

<NewCodeBlock tip="MacOS-host$" type="host">
```
screen /dev/tty.wchusbserial14xx0 1500000
```
</NewCodeBlock>

- 登陆系统

终端内按回车会出现登陆信息，然后使用对应系统的用户账号和密码进行登陆。

终端输入密码不会显示出来，输入完密码按回车登陆。

</TabItem>

</Tabs>

## 系统使用

### 有屏模式

若您是 Radxa ROCK 4D 搭配显示器使用，使用系统就变的比较简单，你可以根据显示器上的系统界面进行操作。

### 无屏模式

若您是 Radxa ROCK 4D 搭配 USB 串口数据线使用，您可以通过串口调试工具进行系统操作。

:::tip
对于无屏模式的用户，我们提供以下建议助力您快速熟悉系统使用。

1. 配置网络

您可以直接给 Radxa ROCK 4D 插入网线，确保系统能够连接网络。

2. 串口调试

您可以通过 [串口调试](../system-config/uart_debug) 查看系统的输出信息，比如 IP 地址、系统启动信息等。

3. 配置 SSH 远程

配置 [SSH 远程](../system-config/ssh-remote) 登录可以去掉 USB 串口数据线，直接使用 SSH 远程登录系统。

4. 配置 VNC 远程

若系统本身带有图形化界面，配置 [VNC 远程](../system-config/vnc-remote) 登录可以让您直接看到系统画面，无需使用显示器。
:::
