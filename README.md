# UCB EECS151 SP22 Mofang's ASIC Lab

<p align="center">
Shi Mofang
</p>
<p align="center">
20202867@cqu.edu.cn
</p>
<p align="center">
Chongqing University
</p>

## Overview

作为一名即将转行进入微电子领域的研0学生，有必要在大四认真学习一下领域的相关基本知识。机缘巧合了解到UCB的EECS151课程，甚合我的口味，于是决定学习一下，争取达到本硕衔接的效果。

## 一、前期准备

### 1、Linux环境搭建

设备型号：`MacBook Pro, 13-inch, 2019, Two Thunderbolt 3 ports`

虚拟机软件：[VMware Fusion](https://www.vmware.com/products/fusion.html)

Linux系统：[Ubuntu(来自清华镜像)](https://mirrors.tuna.tsinghua.edu.cn/ubuntu-releases/)

### 2、Linux基础

教程来自（英文）：[Learning the Shell](http://linuxcommand.org/lc3_learning_the_shell.php)

我的学习笔记&翻译：[Linux基础](asic_lab_1/Linux_Basic.md)

### 3、本系列实验Linux依赖包安装

#### `git`包

教程来自：[如何在 Ubuntu 20.04 上安装 Git](https://zhuanlan.zhihu.com/p/137578868)

`git`软件包被包含在Ubuntu默认的软件源仓库中，并且可以使用 `apt`包管理工具安装。这是在 Ubuntu 上安装`git`最便利，最简单的方式。

以`sudo`权限用户身份运行下面的命令：

```
sudo apt update
sudo apt install git
```

运行下面的命令，打印 `git` 版本，验证安装过程：

```
git --version
```

#### `vim编辑器`

以`sudo`权限用户身份运行下面的命令：

```
sudo apt install vim
```

运行下面的命令，打印 `vim` 版本，验证安装过程：

```
git --version
```

