# USB 网络

大多数radxa产品都预留了一个USB端口作为OTG端口，在运行Android时也作为adb调试端口。你可以在此查阅相应[产品](https://radxa.com/products)的端口定义。
你可以通过OTG端口连接两个产品来建立一个共享网络。现在官方支持最新的linux和android图像。

### 准备工作

**线缆**： 首先，你将需要一条USB-C转USB-C的线来连接两个SBC。

**软件**： 如果你的SBC没有最新的软件，请将你的SBC连接到互联网，并输入以下命令以更新到最新：

```bash
sudo apt update && sudo apt full-upgrade
```

**服务**： 更新软件后，你需要启动`radxa-usbnet`服务：

```bash
sudo systemctl enable --now radxa-usbnet
```

**状态**: 输入以下命令来确认服务是否正常运行：

```bash
sudo systemctl status radxa-usbnet.service
```

服务运行时的活动状态信息为 `active(exited)`。

### OTG设置

首先，用USB-A转USB-A数据线连接两个SBC的OTG端口。
共享网络里的设备性质由你所启用的[overlay](../os-config/rsetup#overlay)决定，主机的设备名称为host。
主机启用此项overlay：

```bash
		[*] Set OTG port to Host mode
```

从机启用此项overlay：

```bash
		[*] Set OTG port to Peripheral mode
```

启用设置后需要重启。

#### 主机设置

为了给设备机共享网络，主机需要连接到外部网络，有线和无线网络都可以。
接下来，我们需要给设备机的连接设置一个共享适配器，在KDE桌面和终端上都可以设置。
此处以在终端设置为例：

**设置共享适配器：**

操作前，请确认是否已经有新的网卡设备：

```bash
ip a
```

它的名称在不同的设备上不同：

```bash
3: enxca5bfb533dd4: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether ca:5b:fb:53:3d:d4 brd ff:ff:ff:ff:ff:ff
    inet6 fe80::b989:8daf:feb5:f020/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```

如果没有新的网卡，你可能需要再次设置overlay或重启。

网络管理器工具(/radxa-os/config/network.md Manager Tool)是推荐的管网络理工具，输入命令即可打开界面：

```bash
sudo nmtui
```

输入密码后，出现设置界面：

```bash
                              NetworkManager TUI

                            Please select an option

                            Edit a connection
                            Activate a connection
                            Set system hostname

                            Quit

                                              <OK>
```

选择 `Edit a connection -- <Add>` 里的 `Ethernet` 项来设置一个适配器：
![add adapter](/img/configuration/add_adapter.webp)
在众多选项中，只需要填写其中的以下两项：

```bash
        Device____  # Enter the third network card name you get by 'ip a', like: enxca5bfb533dd4
        IPv4 CONFIGURATION <Shared> # Change <Automatic> to <Shared>
```

保存配置并返回到设置界面 `Activate a connection`，选择你刚刚添加的选项。
配置好后，则设置会更新为与以下相同：

```bash
                USB Ethernet
                    * Ethernet connection 1
```

**确认适配器设置：**
设置之后，检查是否出现第三张网卡的信息：

```bash
ip a
```

预期的输出结果如下：

```bash
3: enxca5bfb533dd4: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether ca:5b:fb:53:3d:d4 brd ff:ff:ff:ff:ff:ff
    inet 10.42.0.1/24 brd 10.42.0.255 scope global noprefixroute enxca5bfb533dd4
       valid_lft forever preferred_lft forever
    inet6 fe80::e37c:5ced:58a8:ec32/64 scope link noprefixroute
       valid_lft forever preferred_lft forever

```

如果它与你的结果相似，接下来就可以设置从设备了。

#### 从设备设置

**启用usb网络连接：**
相对于主机来说，从设备较容易设置。
首先， 启用 `Set OTG port to Peripheral mode` overlay并且开启 `radxa-usbnet` 服务， 之后重启。
输入 `ip a` 以确认名为 `usb0` 的设备是否被添加到网卡列表:

```bash
3: usb0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc pfifo_fast state DOWN group default qlen 1000
    link/ether 76:c7:9d:9e:d5:da brd ff:ff:ff:ff:ff:ff
```

如果没有，请检查前面的步骤：重新打开Overlay（别忘了重启），并重新启动usbnet服务。

**设置usbnet适配器：**
接下来，像设置主设备一样设置适配器：
打开网络管理器工具：

```bash
sudo nmtui
```

选择 `Edit a connection -- <Add>` 来添加一个 `Ethernet` 适配器：

只需要修改设备选项，输入'usb0'：

```bash
Device usb0
```

其他选项保持默认，保存配置。

**连接到主机设备：**

回到 `Activate a connection`的设置界面，选择你刚刚添加的选项。

```bash
                Ethernet (usb0)
                    Ethernet connection 1
```

连接到主机设备时需要耗费一段时间。

**检查连接情况：**

检查usb0是否被分配了IP地址，如下所示：

```bash
$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN group default qlen 1000
    link/ether f2:44:7d:ac:20:85 brd ff:ff:ff:ff:ff:ff
3: usb0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 76:c7:9d:9e:d5:da brd ff:ff:ff:ff:ff:ff
    inet 10.42.0.46/24 brd 10.42.0.255 scope global dynamic noprefixroute usb0
       valid_lft 3597sec preferred_lft 3597sec
    inet6 fe80::1031:1ee2:bcee:4855/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```

如果主机连接到以太网，从机现在也可以连接到以太网。
