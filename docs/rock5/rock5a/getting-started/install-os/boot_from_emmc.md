---
sidebar_position: 1
---

import Images from "../../\_image.mdx"
import Etcher from '../../../../common/general/\_etcher.mdx';

# 安装系统到 EMMC Module

## 文件下载

<Images loader={false} system_img={true} spi_img={false} />

## EMMC Module 准备

将 [EMMC Module](../../../../accessories/emmc_module.md) 插入到 [EMMC Reader](../../../../accessories/emmc_reader.md) 中，然后将 Reader 插入到 PC 的 USB 端口上

## 镜像烧录

<Etcher model="rock5a" product="Radxa ROCK 5A" pwr_tip={true} power_supply="12V/2A" sd_slot="/img/rock5a/rock5a_with_emmc_module.webp" />

:::tip
系统从上电到开机启动，整个过程持续约 40 秒，然后进入系统桌面。
:::
