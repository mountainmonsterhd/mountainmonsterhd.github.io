---
title: Linux系统环境下安装cuda 10.1 + GTX3090
date: 2021-10-22
description: Linux系统环境下安装cuda，本文以cuda 10.1为例
categories:
  - Linux
  - cuda
  - 环境配置
image: /images/2021_10_22/main.jpg
author_staff_member: 姜流
---
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;此处记录我安装```cuda```环境的经验及遇到的问题。

---

## 版本要求及安装环境确认

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在安装```cuda```之前，需要考虑的是显卡及显卡驱动支持的cuda版本。

查看驱动版本：

```shell

  cat /proc/driver/nvidia/version

```

以下是驱动和```cuda```对应的版本信息：

![Cuda_version](https://mountainmonsterhd.gitee.io/blog.io/images/2021_10_22/P1.png)

本文使用的是```cuda10.1``` 和 显卡驱动```470.74（GTX3090）```

查看显卡使用情况：

```shell

  nvidia-smi

```

* GPU：显卡编号 
* Fan：风扇转速，在0到100%之间变动 
* Name：显卡名
* Temp：显卡温度
* Perf：性能状态，从P0到P12，P0性能最大，P12最小 
* Persistence-M：持续模式的状态开关，该模式耗能大，但是启动新GPU应用时比较快
* Pwr：能耗 
* Bus-Id：涉及GPU总线的东西 
* Disp.A：表示GPU的显示是否初始化 
* Memory-Usage：现存使用率
* GPU-Util：GPU利用率
* Compute M.：计算模式

确认安装环境：

1.```nouveau```是否已经禁用，如果正确安装显卡驱动，则这个是禁用的。

```shell

  lsmod | grep nouveau

```

2.```gcc```安装（尽量保证gcc5.0以上）

```

  gcc --version

```

## 安装过程

这里提供windows和linux的```cuda10.1```百度网盘下载（因为国内在官网下载实在是太慢，且容易失败，此处资源来自网友分享）

**windows**：

链接：```https://pan.baidu.com/s/12Z8X24YY1oVupnkiP5mMPA ```

提取码：417a 

**linux**：

链接：```https://pan.baidu.com/s/1piu7wAjMhl2VrfFEjZZBIA ```

提取码：sxjv 

