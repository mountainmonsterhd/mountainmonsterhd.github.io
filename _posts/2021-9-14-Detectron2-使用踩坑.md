---
title: Detectron2 使用踩坑
date: 2021-09-14
description: 关于我使用Detectron2目标检测框架环境配置踩坑过程
categories:
  - Detectron2
  - 环境配置
  - 目标检测
  - 神经网络
image: /images/2021_9_14/main.jpg
author_staff_member: 姜流
---

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;配置了两周的环境，终于在linux服务器上配置好了环境，成功能够运行基于Detectron2目标检测框架，本文章记录介绍我配置环境遇到并最终解决的问题。

---

## 基本依赖环境

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在安装detectron2框架之前，我们需要基本的python环境以及torch环境。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本文因为需要使用fvcore，fvcore只支持python3.7以上，所以本文使用的python版本是3.7，而detectron2框架使用也尽量用python3.6以上。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;torch版本不能太高也不能太低，也需要根据GPU版本，cuda和cudnn版本进行选择，本文使用的cuda是10.0

查看cuda版本可以使用指令：

```
nvcc -V
```

根据cuda版本使用对应的cudnn版本：

![cuda_cudnn0](https://mountainmonsterhd.gitee.io/blog.io/images/2021_9_14/cuda_cudnn0.png)

![cuda_cudnn1](https://mountainmonsterhd.gitee.io/blog.io/images/2021_9_14/cuda_cudnn1.png)

根据cuda版本选择安装合适的pytorch版本：

| **cuda版本** | **可用torch版本** |
| :----: | :----: |
| 7.5 | 0.4.1, 0.3.0, 0.2.0, 0.1.12-0.1.6 |
| 8.0 | 1.1.0, 1.0.0, 0.4.1 |
| 9.0 | 1.1.0, 1.0.1, 1.0.0, 0.4.1 |
| 9.2 | 1.7.1, 1.7.0, 1.6.0, 1.5.1, 1.5.0, 1.4.0, 1.2.0, 0.4.1 |
| 10.0 | 1.4.0, 1.2.0, 1.1.0, 1.0.1, 1.0.0 |
| 10.1 | 1.7.1, 1.7.0, 1.6.0, 1.5.1, 1.5.0, 1.4.0, 1.3.0 |
| 10.2 | 1.7.1, 1.7.0, 1.6.0, 1.5.1, 1.5.0 |
| 11.0 | 1.7.1, 1.7.0 |
| 11.1 | 1.8.0 |

相对的，python对应的torch版本及torchvision版本：

| **torch版本** | **torchvision版本** | **python版本** |
| :----: | :----: | :----: |
| master/nightly | master/nightly | >=3.6 |
| 1.5.0 | 0.6.0 | >=3.5 |
| 1.4.0 | 0.5.0 | >=2.7, >=3.5, <=3.8 |
| 1.3.1 | 0.4.2 | >=2.7, >=3.5, <=3.7 |
| 1.3.0 | 0.4.1 | >=2.7, >=3.5, <=3.7 |
| 1.2.0 | 0.4.0 | >=2.7, >=3.5, <=3.7 |
| 1.1.0 | 0.3.0 | >=2.7, >=3.5, <=3.7 |
| <=1.0.1 | 0.2.2 | >=2.7, >=3.5, <=3.7 |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;以上并不完全。使用命令行安装：

```shell

  pip install torch==1.4.0 torchvision==0.5.0

```

或者：

```shell

  conda install pytorch==1.4.0

```

或自行手动下载

<a href="https://download.pytorch.org/whl/torch_stable.html">pytorch下载</a>

下载后解压：

```shell

  tar -zxvf （你下载的文件名）

```

进入文件夹使用命令

```shell

  python setup.py install

```

进行安装

需要注意的前提条件，需要gcc/g++且与cuda版本匹配，否则会报错：

```shell

  ERROR: Command errored out with exit status 1: /home/***/anaconda3/envs/detectron2/bin/python3 -c 'import sys, setuptools, tokenize; sys.argv[0] = '"'"'/media/***/69e2e9e1-ea82-4581-8f2c-28660f9a5a91/zjh/detectron2/setup.py'"'"'; __file__='"'"'/media/**/69e2e9e1-ea82-4581-8f2c-28660f9a5a91/zjh/detectron2/setup.py'"'"';f=getattr(tokenize, '"'"'open'"'"', open)(__file__);code=f.read().replace('"'"'\r\n'"'"', '"'"'\n'"'"');f.close();exec(compile(code, __file__, '"'"'exec'"'"'))' develop --no-deps Check the logs for full command output.</p>

```

---

## detectron2安装

使用git下载detectron2，github链接：```https://github.com/facebookresearch/detectron2```

```shell

  git clone https://github.com/facebookresearch/detectron2.git

```

进入到根目录下，使用下列代码可以进行安装，且自动安装所需的依赖环境包：

```shell

  python -m pip install -e detectron2

```

暂时记录到这里，更多问题是因为python版本或pytorch版本问题，不能过高也不能过低。以后遇到别的问题还会进一步记录
