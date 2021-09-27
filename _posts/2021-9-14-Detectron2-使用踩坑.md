---
title: Detectron2 使用踩坑
date: 2021-09-14
description: 关于我使用Detectron2目标检测框架环境配置踩坑过程
categories:
  - Detectron2
  - 环境配置
  - 问题解决
image: images/2021_9_14/main.jpg
author_staff_member: 姜流
---

&nbsp;&nbsp;&nbsp;&nbsp;配置了两周的环境，终于在linux服务器上配置好了环境，成功能够运行基于Detectron2目标检测框架，本文章记录介绍我配置环境遇到并最终解决的问题。

## 基本依赖环境

&nbsp;&nbsp;&nbsp;&nbsp;在安装detectron2框架之前，我们需要基本的python环境以及torch环境。
本文因为需要使用fvcore，fvcore只支持python3.7以上，所以本文使用的python版本是3.7，而detectron2框架使用也尽量用python3.6以上。
torch版本不能太高也不能太低，也需要根据GPU版本，cuda和cudnn版本进行选择，本文使用的cuda是10.0
查看cuda版本可以使用指令：
nvcc -V
根据cuda版本使用对应的cudnn版本。
![cuda_cudnn0](images/2021_9_14/cuda_cudnn0.png)
![cuda_cudnn1](images/2021_9_14/cuda_cudnn1.png)

![Raspberries](https://source.unsplash.com/random/1500x1001)
