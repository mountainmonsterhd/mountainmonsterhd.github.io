---
title: Linux安装mmcv和mmdetection踩坑
date: 2021-10-26
description: 安装mmcv遇到的各种版本问题
categories:
  - mmcv
  - mmdetection
  - 环境配置
  - 目标检测
  - 神经网络
image: /images/2021_10_26/main.jpg
author_staff_member: 姜流
---

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在安装mmcv和mmdetection的时候遇到的各种问题，整体上安装难度并不大，但是要真的配合上cuda和GPU运行起来，则需要考虑更多的版本问题。

---

## 安装过程

在配置好python环境后，可以直接使用

```shell

  pip install mmcv-full

```

进行安装，但是直接安装会在运行时导致和```cuda```版本相关的问题，所以一般是指定版本安装：

```shell

  pip install mmcv-full -f https://download.openmmlab.com/mmcv/dist/{cu_version}/{torch_version}/index.html

```

例如：

```shell

  pip install mmcv-full -f https://download.openmmlab.com/mmcv/dist/cu110/torch1.7.0/index.html

```

其中cu后面的数字是```cuda```版本号，torch后面的数字是```pytorch```版本号。

之后安装mmdetection

首先从github下载（前提是电脑或服务器安装了git）

```shell

  git clone https://github.com/open-mmlab/mmdetection.git

  cd mmdetection

```

然后进行安装：

```shell

  pip install -r requirements/build.txt

  pip install -v -e .  # 或者 "python setup.py develop"

```

这里可以简单的进行测试，在终端输入python进入python终端

输入以下代码：

```shell

  from mmdet.apis import init_detector

```

如果没有报错，则安装成功！

---

## 常见问题

报错：

```shell

  AssertionError: MMCV==1.2.7 is used but incompatible. Please install mmcv＞=1.3.8, ＜=1.4.0.

```

解决方法：

这里表示安装的mmcv版本不对，可以安装后面提示的范围内进行更换版本安装。

可是容易出现下面的错误，这种错误在其他环境配置时，更换了cuda版本，也容易报错报错：

```shell

  ImportError: libcudart.so.10.2:cannot open shared object file: No such file or direct

```

解决方法：

这里提示的就是```cuda```版本不对，如果你不想更换```cuda```版本，那么一般就是mmcv的版本过高或过低，可以直接进入mmcv下载网站手动下载库的安装包：

https://download.openmmlab.com/mmcv/dist/cu110/torch1.7.0/index.html

或

https://download.openmmlab.com/mmcv/dist/


找到你需要的mmcv的版本，复制连接，在终端使用

```shell

  wget （你复制的链接）

```

进行下载。

再使用

```shell

  pip install （你下载的文件）

```

进行安装

我的环境是```cuda11.1+torch1.10.0```

所以下载的是：

```https://download.openmmlab.com/mmcv/dist/cu111/torch1.10.0/index.html```