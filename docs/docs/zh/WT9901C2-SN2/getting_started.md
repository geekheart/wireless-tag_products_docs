---
title: WT9901C2-SN2 新手指南
tags: WT9901C2-SN2, esp32c2
keywords: WT9901C2-SN2, esp32c2, ESP32C2, esp32-c2, ESP32-C2
update:
  - date: 2025-06-26
    author: 沧御
    version: 1.0.0
    content: 首次更新文档
---

## 如何烧录 AT 固件

### 准备工作

`WT9901C2-SN2` 开发板在进行固件烧录时软硬件如下：

- 硬件设备：
  - `WT9901C2-SN2` 开发板 x 1
  - `TypeC USB` 线 x 1
  - 个人电脑（操作系统支持 `Windows 7` [64 位]、`Windows 10`， `Windows 11`） x 1
- 软件设备：
  - [AT 固件](/docs/assets/common/ESP32-C2-2MB-AT-V3.1.0.0.zip) x 1
  - [烧录上位机工具](https://dl.espressif.com/public/flash_download_tool.zip) x 1

### 入口页面

打开烧录上位机工具，双击 `.exe` 文件后进入工具的入口界面，切换 `ChipType` 为 `esp32c2` 如下图所示

<div style="text-align: center; padding: 20px; border-radius: 12px;">
  <img src="/docs/assets/WT9901C2-SN2/烧录上位机入口页面.jpeg" 
       alt="烧录上位机入口页面"
       style="display:block; margin:0 auto; max-width:100%; border: 1px solid #eee; box-shadow: 0 2px 8px rgba(0,0,0,0.08);">
  <lable style="font-style: italic;">烧录上位机入口页面</label>
</div>

点击确定，进入烧录主页面

### 选择 AT 固件进行烧录

通过 `TypeC USB` 线连接单片机和电脑，并找到其串口号。

解压下载的[AT 固件](/docs/assets/common/ESP32-C2-2MB-AT-V3.1.0.0.zip)，并配置烧录上位机，如下图所示：

<div style="text-align: center; padding: 20px; border-radius: 12px;">
  <img src="/docs/assets/WT9901C2-SN2/烧录AT固件.jpeg" 
       alt="烧录AT固件"
       style="display:block; margin:0 auto; max-width:100%; border: 1px solid #eee; box-shadow: 0 2px 8px rgba(0,0,0,0.08);">
  <lable style="font-style: italic;">烧录AT固件</label>
</div>

点击 `START` 即可进行烧录

打开串口工具，配置好串口号等设置：

- 波特率：115200
- 数据位：8
- 校验位：None
- 停止位：1
- 流控：None
- 输入 “AT+GMR” 命令，并且换行（CRLF）
  如果结果如下图所示，则表示成功：

<div style="text-align: center; padding: 20px; border-radius: 12px;">
  <img src="/docs/assets/WT9901C2-SN2/烧录成功后AT回复.jpeg" 
       alt="烧录成功后AT回复"
       style="display:block; margin:0 auto; max-width:100%; border: 1px solid #eee; box-shadow: 0 2px 8px rgba(0,0,0,0.08);">
  <lable style="font-style: italic;">烧录成功后AT回复</label>
</div>

## 如何搭建 ESP-IDF 并编译烧录 Hello World 例程

1. 通过[乐鑫官方教程](https://docs.espressif.com/projects/esp-idf/zh_CN/latest/esp32c2/get-started/index.html)搭建环境

2. 复制 `examples/get-started/hello_world/` 文件夹到当前。
3. 激活 `esp-idf` 环境

```shell
Done! You can now compile ESP-IDF projects.
Go to the project directory and run:

  idf.py build
```

4. 切换到 `esp32c2` 目标上

```shell
idf.py set-target esp32c2
```

5. 编译 `hello world` 工程

```shell
idf.py build
```

6. 烧录 `hello world` 

```shell
idf.py flash -p <PORT>
```

7. 打开串口监视器 `hello world`

```shell
idf.py monitor -p <PORT>
```

## 如何将 WT9901C2-SN2 当作烧录器给其它开发板烧录

将 `EN` 和 `GND` 通过短接帽进行短接。开发板即可作为烧录器或者串口监视器使用。如下图所示：
<div style="text-align: center; padding: 20px; border-radius: 12px;">
  <img src="/docs/assets/WT9901C2-SN2/开发板烧录器接线.jpeg" 
       alt="开发板烧录器接线"
       style="display:block; margin:0 auto; max-width:100%; border: 1px solid #eee; box-shadow: 0 2px 8px rgba(0,0,0,0.08);">
  <lable style="font-style: italic;">开发板烧录器接线</label>
</div>
