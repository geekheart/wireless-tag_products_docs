---
title: WT3299P4-TINY 新手指南
tags: WT3299P4-TINY, esp32p4
keywords: WT3299P4-TINY, esp32p4, esp32-p4, ESP32P4, ESP32-P4
update:
  - date: 2025-09-10
    author: 沧御
    version: 1.0.0
    content: 首次更新文档
---

## 搭建 ESP32-P4 开发环境

本教程主要介绍如何在 windows 环境下使用 WSL2 编译 idf 环境。其主要优点如下：

- 在 ubuntu 的环境编译比 windows 环境下效率高
- WSL2 比虚拟机可以更加的合理使用 windows 资源
- 环境和 Windows 互通，文件的传输比虚拟机更加好用

### 准备工作

- 一款 ESP32-P4 开发板
- USB 数据线 （A 转 Type-C）
- 电脑（Windows、Linux 或 macOS）

### 安装 WSL2

1. 以管理员身份打开命令提示符或 PowerShell。

2. 输入以下命令：

```shell
wsl --install
```

3. 系统会自动下载并安装所需的组件，并默认安装 Ubuntu 发行版。

4. 安装usbipd工具用于挂载windows的开发板设备
[WSL-USB-GUI](https://gitlab.com/alelec/wsl-usb-gui/-/releases)
下载`WSL-USB-x.x.x.msi`,双击安装。

### 安装 IDF

1. 安装以下的软件包：

```shell
sudo apt-get install git wget flex bison gperf python3 python3-pip python3-venv cmake ninja-build ccache libffi-dev libssl-dev dfu-util libusb-1.0-0
```

2. 获取 ESP-IDF：

```shell
mkdir -p ~/esp
cd ~/esp
git clone -b v5.4.2 --recursive https://github.com/espressif/esp-idf.git
```

3. 安装编译工具链：

```shell
cd ~/esp/esp-idf
export IDF_GITHUB_ASSETS="dl.espressif.com/github_assets"
./install.sh
```

4. 设置环境变量：

将以下内容加入到.bashrc中后重启终端
```shell
alias get_idf='. $HOME/esp/esp-idf/export.sh'
```

### 编译LED闪烁例程

1. clone 例程仓库，并进入blink例程

```shell
git clone https://github.com/wireless-tag-com/WT9932P4-TINY
cd WT9932P4-TINY/blink/
```

2. 激活idf环境

```shell
get_idf
```

3. 设置idf

```shell
idf.py set-target esp32p4
```

4. 编译blink

```shell
idf.py build
```

5. USB线连接WT9932P4-TINY的FUSB，打开`WSL-USB-GUI`挂载到WSL中

6. 烧录blink

```shell
idf.py flash -p /dev/ttyACM0
```

### 现象
你会看到板载的LED呈现白光闪烁