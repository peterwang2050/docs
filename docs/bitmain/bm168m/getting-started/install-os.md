---
sidebar_position: 2
sidebar_label: 系统安装
title: 系统安装
---

本文档将介绍如何把 OS 镜像安装到 bm168m 中。

## 准备工作

- 1x microSD 卡(容量 >=8GB)
- 1x microSD 读卡器
- 20V 电源适配器（在整机下安装系统镜像，整机供电20V）
- usb type-a转type-c数据线一条（日志输出）

## 镜像下载

请到 [快速上手下的资源下载汇总](/bitmain/aicore-bm1684x/download.md)下载对应的镜像文件

## 系统安装

### 1.格式化SD卡

请将 SD 卡格式化为 FAT32 格式（如果 SD 卡上有多个分区，只能使用第一个分区），大小
为 1GB 以上。下面介绍使用linux命令fdisk和windows下使用工具格式化SD卡，如果SD卡原本就有分区请先将分区进行删除.

### linux

```
$ sudo fdisk /dev/sda
Welcome to fdisk (util-linux 2.37.2).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

# d是删除分区命令
Command (m for help): d
Selected partition 1
Partition 1 has been deleted.

# n是新建分区命令
Command (m for help): n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p): # 回车即可

Using default response p.
Partition number (1-4, default 1): # 回车即可
First sector (2048-125173759, default 2048): # 回车即可
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-125173759, default 125173759): +3G # 指定新建分区为3G大小，只要大于1G即可

Created a new partition 1 of type 'Linux' and of size 3 GiB.
Partition #1 contains a vfat signature.

Do you want to remove the signature? [Y]es/[N]o: y # 不沿用之前的分区文件系统类型

The signature will be removed by a write command.

Command (m for help): wq # 保存退出
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```

使用mkfs.vfat命令将分区格式化为fat32格式

```
$ sudo mkfs.vfat /dev/sda1
mkfs.fat 4.2 (2021-01-31)
```

### windows

使用工具rufus，[安装链接](https://rufus.ie/)

按照下图步骤格式化sd卡

<img
  src="/img/aicore-bm1684x/rufus-use.webp"
  alt="radxa-aicore-bm1684x interfaces"
/>

### 2.将下载的压缩包解压，并将里面的所有文件拷贝到 SD 卡根目录

确认文件如下

<img src="/img/aicore-bm1684x/img.webp" alt="radxa-aicore-bm1684x interfaces" />

### 3.SD卡刷机

请将 Fogwise BM168M 断电，插入 SD 卡，并连接串口终端（使用usb type-a转type-c数据线，type-c接 Fogwise BM168M 的debug口，type a连接电脑，波特率设置成115200，debug口位置在[Fogwise BM168M硬件信息下的硬件接口说明](../../bm168m/hardware-design/hardware-interface.md)寻找），然后给整机上电。您将看到
BM1684X 自动进入刷机流程：

```
Hit any key to stop autoboot:  0
switch to partitions #0, OK
mmc1 is current device
Scanning mmc 1:1...
Found U-Boot script /boot.scr
fs reading /boot.scr
891 bytes read in 5 ms (173.8 KiB/s)
## Executing script at 300040000
Setting bus to 1
LED 'status' not found (err=-19)
LED 'error' not found (err=-19)
update SPI flash
fs reading //boot_spif.scr
746 bytes read in 5 ms (145.5 KiB/s)
## Executing script at 300040000
fs reading //spi_flash.bin
5385980 bytes read in 673 ms (7.6 MiB/s)
SF: Detected gd25lq128 with page size 256 Bytes, erase size 4 KiB, total 16 MiB
chip_type=bm1684x
device 0 offset 0x0, size 0x200000
0 bytes written, 2097152 bytes skipped in 2.844s, speed 754032 B/s
SPI flash update done
update eMMC
```

刷机通常耗时约 3 分钟，结束后，会看到拔掉 SD 卡并重启 BM1684X 的提示，请依照操作
即可：

```
eMMC update done
bm savelog 449 bytes written in 10 ms (43 KiB/s)
all done
LED 'status' not found (err=-19)
LED 'error' not found (err=-19)
LED 'status' not found (err=-19)
Please remove the installation medium, then reboot
LED 'status' not found (err=-19)
```

:::tip
如果出现烧录过程失败，一般是芯片发烫导致的，这时请等待芯片降温到一定程度再重新上电进入刷机流程
:::

## 系统启动

- 按照上述步骤成功烧录镜像到emmc后，将 microSD 卡拔出，然后给 Fogwise BM168M 上电。

## 注意事项

关机时建议使用 sudo poweroff 命令，尽量避免直接断电，以免文件系统损坏。
